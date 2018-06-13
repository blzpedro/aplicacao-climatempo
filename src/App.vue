<template>
  <div>
    <cabeca></cabeca>
    <div id="mid">
      <input type="text" v-model="pesquisa" placeholder="ex: Santos">
      <button v-on:click="geraJSON">Pesquisar</button>
    </div>
  </div>
</template>

<script>
import Cabeca from './assets/components/shared/header/Cabeca.vue';

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
          
			    alert(dados);
			
			}, response => {
                alert("Cidade não encontrada.");
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
