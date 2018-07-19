<template>
  <div id="app">
    <div class="img-container">
      <img src="./assets/skyDive.jpg">
    </div>
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
  .img-container{
    width: 300px;
    height: 300px;
    border-radius: 50% ;
    overflow: hidden;
  }
.img-container img{
  width: 100%;
}
</style>
