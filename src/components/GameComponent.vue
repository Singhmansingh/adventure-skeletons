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
  justify-content: center;
  align-items: center;
}
</style>
