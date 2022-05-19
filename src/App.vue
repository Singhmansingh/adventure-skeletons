<template>
  <HeaderComponent/>
  <GameComponent/>
  <FooterComponent/>
</template>

<script>
import GameComponent from './components/GameComponent.vue'
import HeaderComponent from './components/HeaderComponent.vue'
import FooterComponent from './components/FooterComponent.vue'
export default {
  name: 'App',
  components: {
    GameComponent,
    HeaderComponent,
    FooterComponent
    
  }
}
</script>

<style>
@font-face {
  font-family: "Skeleton";
  src: url("./assets/fonts/Headhunter.ttf");
}
@font-face {
  font-family: "Spooky";
  src: url("./assets/fonts/RestlessSoulBB-Regular.otf");
}
#app {
  font-family: "Spooky", serif;
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

 select {
    background: white;
    border: 2px solid rgb(17, 17, 17);
    color:rgb(17, 17, 17);
    width: 90%;
    height: 30px;
    text-align: center;
    font-family: inherit;
            font-size: 1.3em;
    padding:0;

}
option {
    font-size: 0.75em;
    color:white;
    background-color: rgb(43, 43, 43);
}
</style>
