<template>
  <div>
    <cabeca></cabeca>
    <div id="mid">
      <input type="text" v-model="pesquisa" placeholder="ex: Santos">
      <button v-on:click="geraJSON">Pesquisar</button>
      <p>{{ status }}</p>
    </div>
  </div>
</template>

<script>
import Cabeca from './assets/components/shared/header/Cabeca.vue';


      /***
      * DESCRICAO: Essa funcao recebe um json com os dados do clima da cidade especificada e cria um painel na pagina index.html
      * AUTOR: Henrique / Gabriel / Pedro
      * ENTRADA : Recebe o objeto da funcao geraJSON
      * SAIDA: 
      ***/
function preencheDados(dados){

    var clima = dados;
    
    var divInfo = document.createElement('div');
    var divTop = document.createElement('div');
    divInfo.setAttribute('id', 'painel');
    var imgClima = document.createElement('img');
    var pNome = document.createElement('h2');
    pNome.setAttribute('id', 'painel-titulo');
    var pTemp = document.createElement('p');
    var pTempmax = document.createElement('p');
    var pTempmin = document.createElement('p');
    imgClima.src = "http://openweathermap.org/img/w/" +  clima.weather[0].icon + ".png"
    pNome.innerHTML = clima.name;
    pTemp.innerHTML = "Temperatura atual: " + clima.main.temp.toFixed(1);
    pTempmax.innerHTML = "Temperatura máxima: " + clima.main.temp_max.toFixed(1);
    pTempmin.innerHTML = "Temperatura mínima: " + clima.main.temp_min.toFixed(1);
    divInfo.appendChild(pNome);
    divInfo.appendChild(pNome);
    divInfo.appendChild(pTemp);
    divInfo.appendChild(pTempmax);
    divInfo.appendChild(pTempmin);
    divInfo.appendChild(imgClima);
    document.body.appendChild(divInfo);
}


export default {
    components: {
      'cabeca': Cabeca, 
    },
    
    data() {
      return {
      pesquisa: ''
    };
  },
  
  methods:{
    
      /***
      * DESCRICAO: Funcao que faz a requisicao da api e retorna um json com os dados, caso nao encontra a cidade dispara um alert.
      * AUTOR: Henrique
      * ENTRADA :
      * SAIDA: JSON
         ***/
      geraJSON: function () {
      
        this.$http.get('http://api.openweathermap.org/data/2.5/weather?q=' + this.pesquisa + '&APPID=d88c03f3eb8efe8c97422955694012c9&lang=pt&units=metric')
        .then(res => res.json())
        .then(dados => {
          
			    preencheDados(dados);
			
			}, response => {
               alert("Cidade nao encontrada");
        });
      
    }
  }
};
</script>

<style>
*{
box-sizing: border-box;
}
body {
font-family: Helvetica, Verdana;
margin: 0;
background-image: url("img/ceu.png");
background-size: 100%;
background-repeat: no-repeat;
}

#mid{
    text-align: center;
}

button{
    width: 100px;
    height: 55px;
    background-color: #80d4ff;
    border-style: none;
    font-size: 16px;
    font-weight: 600;
}

button:hover{
    transition-duration: 0.6s;
    background-color: #0066ff;

}

input{
    height: 51px;
    border: none;
    border-bottom: 2px solid black;
    font-size: 20px;
    opacity: 0.8;
}
</style>
