<template>
  <div id="app">
    <!-- <img src="./assets/logo.png"> -->
    <!-- <dialog-a></dialog-a> -->
    <fly></fly>
    <!-- <el-button>ad</el-button> -->
  </div>
</template>

<script>
import Fly from './components/fly'
// import dialog from './components/dialog'
export default {
  name: 'App',
  components:{
    'fly':Fly,
    // 'dialog-a':dialog
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
  margin-top: 60px;
}
</style>
