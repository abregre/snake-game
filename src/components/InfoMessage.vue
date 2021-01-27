<template>
  <div class="overlay">
    <div class="card">
      <h3 :class="username ? 'mb-1' : ''">
        Game Over! {{ username ? capitalize(username) : 'Loser' }} your score
        was {{ score }}
      </h3>
      <small v-if="!username" class="mb-1"
        >*If you don't wanna get called Loser, set a username</small
      >
      <button @click="playAgain" class="btn mb-1">Play Again</button>
      <button @click="close" class="btn">Show Rankings</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    username: String,
    score: Number,
    playAgain: Function,
    capitalize: Function,
    close: Function,
  },
}
</script>

<style scoped>
.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  z-index: 1;
  background: rgba(0, 0, 0, 0.486);
  display: flex;
  justify-content: center;
  align-items: center;
}
.card {
  width: 400px;
  height: 300px;
  background: #fff;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  z-index: 2;
}
h3 {
  position: relative;
  z-index: 3;
  margin: 0;
}
small{
  color: rgb(248, 75, 75);
}
</style>
