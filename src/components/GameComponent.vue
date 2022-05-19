<template>
<div id="container">
    <PlayerComponent v-for="player in players" :key="'player-'+player"/>
</div>
</template>

<script>
import PlayerComponent from './PlayerComponent.vue'
export default {
  name: 'HelloWorld',
  components:{
    PlayerComponent
  },
  mounted(){
    window.addEventListener("keyup", (e)=>{
      if(e.key == '[' && this.players > 1) this.players--;
      else if(e.key == ']' && this.players < 6) this.players++;
    })
  },
  data(){
    return {
      players:1
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#container{
  flex:3;
  background: rgb(24, 24, 24);
  display: flex;
  justify-content: space-evenly;
  align-items: center;
}
</style>
