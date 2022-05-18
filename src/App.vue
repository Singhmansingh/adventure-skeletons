<template>
  <HeaderComponent/>
  <GameComponent/>
</template>

<script>
import GameComponent from './components/GameComponent.vue'
import HeaderComponent from './components/HeaderComponent.vue'
export default {
  name: 'App',
  components: {
    GameComponent,
    HeaderComponent
    
  }
}
</script>

<style>

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  background: #141414;
  flex:1;
  padding: 10px;
  display:flex;
  flex-direction: column;
  box-sizing: border-box;
}
body {
  display: flex;
  margin: 0;
  height: 100vh;
  width: 100vw;
  overflow: hidden;

}
</style>
