<template>
    <div>
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
</style>