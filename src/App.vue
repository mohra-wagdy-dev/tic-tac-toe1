<template>
  <div id="App">
    <h1>Tic-Tac-Toe Game</h1>
    <h2>hi kirolos nabil</h2>
    <BaseGrid />
  </div>
</template>

<script>
import BaseGrid from "./components/BaseGrid.vue";
export default {
  name: "App",
  components: {
    BaseGrid,
  },
  data(){
   return{
    matches: 0,
    wins:{
      O: 0,
      X: 0,
    }
   }

  }
};
</script>

<style scoped>
#app{
font-family: Georgia, 'Times New Roman', Times, serif;
text-align: center;
color: cadetblue;
margin: 0 auto;
max-width: 400px;
}
#app h1{
  text-transform: uppercase;
  font-weight: bold;
font-size: 3em;
}
</style>
