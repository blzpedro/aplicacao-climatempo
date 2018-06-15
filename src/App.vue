<template>
  <div>
    <cabeca></cabeca>
    <div id="mid">
      <input id="campo"  type="text" v-model="pesquisa" placeholder="ex: Santos">
      <button v-on:click="geraJSON">Pesquisar</button>
      <button v-on:click="limpar" >Limpar</button>
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
      
function preenchePainel(dados){

    var clima = dados;
    
    var divInfoAtual = document.createElement('div');
    divInfoAtual.setAttribute('id', 'painel');
    divInfoAtual.setAttribute('class', 'principal');
    var imgClima = document.createElement('img');
    var imgTemp = document.createElement('img');
    var imgTempMin =  document.createElement('img');
    var imgTempMax = document.createElement('img');
    var imgUmidade = document.createElement('img');
    var imgVento = document.createElement('img');
    var pNome = document.createElement('h2');
    pNome.setAttribute('id', 'painel-titulo');
    pNome.setAttribute('class', 'pnome')
    var pTemp = document.createElement('p');
    var pTempmax = document.createElement('p');
    var pTempmin = document.createElement('p');
    var pDescricao = document.createElement('p');
    pDescricao.setAttribute('style', 'margin-left:37%');
    var pUmidade = document.createElement('p');
    var pVelvento = document.createElement('p');
    var pSigla = document.createElement('h4');
    pSigla.setAttribute('style', 'display: inline; margin: 10px;')
    imgClima.src = "http://openweathermap.org/img/w/" +  clima.list[0].weather[0].icon + ".png";
    imgTempMax.src = "img/max.png";
    imgUmidade.src = "img/umidade.png";
    imgVento.src = "img/vento.png";
    imgTemp.src = "img/tempatual.ico";
    imgTempMin.src = "img/azul.png";
    pNome.innerHTML = clima.city.name;
    pTemp.innerHTML = "Temperatura atual: " + clima.list[0].main.temp.toFixed(1);
    pTempmax.innerHTML = "Temperatura máxima: " + clima.list[0].main.temp_max.toFixed(1);
    pTempmin.innerHTML = "Temperatura mínima: " + clima.list[0].main.temp_min.toFixed(1);
    pUmidade.innerHTML = "Umidade: " + clima.list[0].main.humidity +"%";
    pVelvento.innerHTML = "Ventos: " + (3.6 * clima.list[0].wind.speed).toFixed(2) + " km/h";
    pDescricao.innerHTML = "Descrição: " + clima.list[0].weather[0].description;
    pSigla.innerHTML = clima.city.country;
    divInfoAtual.appendChild(pNome);
    divInfoAtual.appendChild(pTemp);
    pTemp.appendChild(imgTemp);
    pTempmax.appendChild(imgTempMax);
    divInfoAtual.appendChild(pTempmax);
    divInfoAtual.appendChild(pTempmin);
    pTempmin.appendChild(imgTempMin);
    pUmidade.appendChild(imgUmidade);
    divInfoAtual.appendChild(pUmidade);
    divInfoAtual.appendChild(pVelvento);
    pVelvento.appendChild(imgVento);
    divInfoAtual.appendChild(pDescricao);
    pNome.appendChild(imgClima);
    pNome.appendChild(pSigla);
    document.body.appendChild(divInfoAtual);
}

      /***
      * DESCRICAO: Essa funcao percorre o JSON
      * AUTOR: Henrique
      * ENTRADA : Recebe o parametro da funcao criaDiv e da API 
      * SAIDA: 
      ***/
      
  function preenchePainelPrevisao(dados){
    
    for (var i = 8; i < dados.cnt; i++) { 
      criaPainel(dados,i);
      i=i+7;
    }
  
  }


      /***
      * DESCRICAO: Como a api retorna a data no formato AA/MM/DD essa funcao ira converter para DD/MM
      * AUTOR: Henrique / Gabriel
      * ENTRADA : Recebe o JSON e um contador
      * SAIDA: Retorna a data convertida
      ***/  
  function converteData(dados,x){
  
    var data = dados.list[x].dt_txt.substring(5,10);
    var mes='';
    var dia='';
    
    for(var i = 3 ; i <= 4; i++){
          dia = dia + data[i];
    }
    
    for(var i = 0 ; i < 2; i++){
          mes = mes + data[i];
    }
  
    return (dia + '/' + mes);
    
  }


      /***
      * DESCRICAO: Essa funcao recebe um json com os dados do clima da cidade pesquisada e cria um painel com as informações dos próximos 5 dias
      * AUTOR: Henrique / Gabriel / Pedro
      * ENTRADA : Recebe o objeto da funcao geraJSON e o indice do objeto JSON
      * SAIDA: 
      ***/
      
 function criaPainel(dados,x){

    var data = dados.list[x].dt_txt;
    
    var divInfo = document.createElement('div');
    divInfo.setAttribute('id', 'painel');
    divInfo.setAttribute('style', 'margin: 30px 10px 0 5%;')
    var pTemp = document.createElement('p');
    var pTempmax = document.createElement('p');
    var pTempmin = document.createElement('p');
    var pUmidade = document.createElement('p');
    var h2Data = document.createElement('h4');
    var h2Prev = document.createElement('h2');
    h2Prev.setAttribute('id', 'painel-titulo');
    var imgTemp = document.createElement('img');
    var imgTempMin =  document.createElement('img');
    var imgTempMax = document.createElement('img');
    var imgUmidade = document.createElement('img');
    h2Prev.innerHTML = "Previsão para:";
    pTemp.innerHTML = "Temperatura média: " + dados.list[x].main.temp.toFixed(1) + " C°";
    pTempmax.innerHTML = "Temperatura máxima: " + dados.list[x].main.temp_max.toFixed(1) + " C°";
    pTempmin.innerHTML = "Temperatura mínima: " + dados.list[x].main.temp_min.toFixed(1) + " C°";
    pUmidade.innerHTML = "Umidade: " + dados.list[x].main.humidity + "%";
    imgTempMax.src = "img/max.png";
    imgUmidade.src = "img/umidade.png";
    imgTemp.src = "img/tempatual.ico";
    imgTempMin.src = "img/azul.png";
    h2Data.innerHTML = converteData(dados,x);
    divInfo.appendChild(h2Prev);
    h2Prev.appendChild(h2Data);
    divInfo.appendChild(pTemp);
    divInfo.appendChild(pTempmax);
    pTemp.appendChild(imgTemp);
    pTempmax.appendChild(imgTempMax);
    divInfo.appendChild(pTempmin);
    divInfo.appendChild(pUmidade);
    pTempmin.appendChild(imgTempMin);
    pUmidade.appendChild(imgUmidade);
    document.body.appendChild(divInfo);
 
}


export default {
    components: {
      'cabeca': Cabeca, 
    },
    
    data() {
      return {
      pesquisa: '',
    };
  },
  
  methods:{
    
          
      /***
      * DESCRICAO: Função para remover os painéis das cidades pesquisadas.
      * AUTOR: Gabriel
      * ENTRADA : 
      * SAIDA:
      ***/
      limpar: function() {
        
        while ('painel.value' != 0 ){
          document.getElementById('painel').remove();
        }
      },
    
    
      /***
      * DESCRICAO: Funcao que faz a requisicao da api e retorna um json com os dados, caso nao encontra a cidade dispara um alert.
      * AUTOR: Henrique
      * ENTRADA :
      * SAIDA: JSON
         ***/
   
    geraJSON: function () {
      
        this.$http.get('http://api.openweathermap.org/data/2.5/forecast?q=' + this.pesquisa + '&APPID=d88c03f3eb8efe8c97422955694012c9&lang=pt&units=metric')
        .then(res => res.json())
        .then(dados => {
          
          this.pesquisa ='';
          this.status='';
          document.getElementById('campo').value='';
          preenchePainel(dados);
          preenchePainelPrevisao(dados);
			
			}, response => {
                alert("A Cidade "+ this.pesquisa + " nao foi encontrada" );
                document.getElementById('campo').value='';
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
    background-attachment: fixed;
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

#painel {
    padding: 0 auto;
    border: solid 2px grey;
    display: inline-block;
    box-shadow: 3px 5px 5px grey;
    height: auto;
    vertical-align: top;
    text-align: center;
    background-color: #d9d9d9;
}

#painel #painel-titulo {
    text-align: center;
    border: solid 1px;
    background: lightblue;
    margin: 0 0 20px 0;
    padding: 0;
    text-transform: uppercase;
    height: 60px;
    width: 100%;
    display: inline-table;
} 

p{
    margin-top: 20px;
    font-size: 14px;
    font-weight: bold;
}

div p{
    text-align: left;
    margin-left: 10px;
    margin-top: 10px;
    padding: 10px 0;
}

h2 img{
    float: left;
    height: 100px;
    width: 100px;
    margin-right: -80px;
}

#painel p img{
  position: relative;
  bottom: 10px;
  width: 30px;
  float: left;
  margin-right: 5px;
  margin-top: 7px;
}

#painel p:first-child{
  margin-top: 50px;
}

h4{
  margin: 10px 0;
}

.principal{
  width: 70%;
  margin: 20px 15%;
}

.principal p{
  font-size: 22px;
  margin: 3px;
}

.principal p img{
  margin-left: 33%;
}

.pnome{
  font-size: 35px;
}

.pnome h2{
  position: relative;
  top: 20px;
}
</style>
