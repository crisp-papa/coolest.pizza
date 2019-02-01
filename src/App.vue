<template>
  <div id="app">
    <div class="placeholder">

    </div>
    <MusicPlayer/>
  </div>
</template>

<script>
import MusicPlayer from './components/MusicPlayer.vue'

export default {
  name: 'app',
  components: {
    MusicPlayer,
  }
}
</script>

<style lang="less">
* { 
  box-sizing: border-box;
}
body { 
  background-color: rgb(13, 29, 68);
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #fff;
  margin-top: 60px;
}
.placeholder { 
  width: 70%; 
  display: inline-block;
}
</style>
