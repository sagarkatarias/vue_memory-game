<template>
  <div id="app">
    <GameBoard class="game-area" :columns="4" />
  </div>
</template>

<script>
import GameBoard from './components/GameBoard.vue';

export default {
  name: 'App',
  components: {
    GameBoard
  },
  props: {
    columns: {
      type: Number,
      default: 4
    }
  }
};
</script>

<style>
body {
  margin: 0;
  background: radial-gradient(#485563, #29323c);
  color: white;
}

html {
  min-height: 100vh;
}

#app {
  font-family: 'Poppins', Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 50px;
}

.game-area {
  max-width: 600px;
  margin: auto;
}
</style>
