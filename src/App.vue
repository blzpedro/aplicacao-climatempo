<template>
  <div>
    <cabeca></cabeca>
    <div>
      <input type="text" placeholder="ex: Santos">
      <button>Pesquisar</button>
    </div>
  </div>
</template>

<script>
import Cabeca from './assets/components/shared/header/Cabeca.vue';

export default {
    components: {
      'cabeca': Cabeca, 
    }
}
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
