<template>
  <div class="overlay">
    <div class="card">
      <h3>Game Over! {{capitalizeName(username)}} your score was {{ score }}</h3>
      <button @click="playAgain">Play Again</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    username: String,
    score: Number,
    playAgain: Function,
  },
  methods: {
      capitalizeName(name){
          return name.charAt(0).toUpperCase() + name.slice(1)
      }
  }
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
}
</style>
