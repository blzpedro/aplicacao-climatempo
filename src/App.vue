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


</style>
