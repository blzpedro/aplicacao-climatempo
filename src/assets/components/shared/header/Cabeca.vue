<template>
    <div>
        <a href="https://www.openweathermap.org/">
            <img src="img/api-icon.png" id="iconapi">
        </a>
        <a href="https://vuejs.org/">
            <img src="img/vue.png" id="vueapi">
        </a>
        <div id="bg1">
            <h1>{{ titulo }}</h1>
        </div>
            <h3>{{ subtitulo }}</h3>
    </div>
</template>

<script>
export default {
  data() {
    return {
      titulo: 'Climatempo',
      subtitulo: 'Digite uma cidade no campo abaixo:'
    }
  }
};
</script>

<style>
#bg1{
    background: linear-gradient(to right, #ccffff, #99ccff, #3399ff, #0066ff); 
    margin-top: 0;
    height: 80px;
}

#bg1 h1{
    margin: 0;
    position: relative;
    top: 20px;
    text-align: center;
}

h3{
    text-align: center;
}

#iconapi{
    width: 95px;
    float: left;
}

#vueapi{
    width: 100px;
    float: right;
}
</style>