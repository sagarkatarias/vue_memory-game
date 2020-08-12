<template>
  <div class="dashboard">
    <template v-if="turns">
      <h3>Turns: {{ turns }}</h3>
      <button v-on:click="createBoard">Start a new game</button>
    </template>
    <template v-if="finishGame">
      <h3>Congratulations!! You found all cards</h3>
    </template>
  </div>
</template>

<script>
export default {
  props: ['turns', 'finishGame', 'createBoard']
};
</script>

<style scoped>
.dashboard {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin: 5px;
}

.dashboard button {
  color: #fff !important;
  text-transform: uppercase;
  text-decoration: none;
  background: #708090;
  padding: 10px;
  border-radius: 5px;
  display: inline-block;
  border: none;
  transition: all 0.4s ease 0s;
}
.dashboard button:hover {
  background: #2a2a2a;
  letter-spacing: 1px;
  -webkit-box-shadow: 0px 5px 40px -10px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 5px 40px -10px rgba(0, 0, 0, 0.57);
  box-shadow: 5px 40px -10px rgba(0, 0, 0, 0.57);
  transition: all 0.4s ease 0s;
}
</style>
