<template>
  <div id="app">
    <!-- <i class="iconfont icon-jinrudianpu"></i> -->
    <leftNav></leftNav>
    <div class="main">
      <router-view/>
    </div>
    
  </div>
</template>

<script>
import leftNav from './components/common/leftNav'
export default {
  name: 'App',
  components:{
    leftNav
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /*height: 100%;*/
/*  margin-top: 60px;*/
}
.main{
  float: left;
  width: 95%;
  background-color: #Eff2f7;
  height: 100%;
  overflow: hidden;
}
</style>
