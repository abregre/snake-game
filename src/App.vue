<template>
  <h1>Snake Game</h1>
  <div class="container">
    <div class="col">
      Cell size (px):
      <input type="number" min="10" v-model.number="cellSize" />
    </div>
    <div class="col">
      Board size (cells):
      <input type="number" min="5" v-model.number="boardSize" />
    </div>
    <div class="col">
      Speed:
      <input type="number" min="1" v-model.number="speed" />
    </div>
  </div>
  <div class="container">
    <snake-canvas :cellSize="cellSize" :boardSize="boardSize" :speed="speed" :isPlaying="isPlaying" />
  </div>
  <div class="container">
    <div class="controls">
      <div class="scores">Scores: {{ scores }}</div>
      <button class="play-btn" @click="gameBtn">{{ isPlaying ? 'Stop' : 'Play' }}</button>
    </div>
  </div>
</template>

<script>
import SnakeCanvas from './components/SnakeCanvas.vue'
export default {
  name: 'App',
  components: { SnakeCanvas },
  data() {
    return {
      cellSize: 10,
      boardSize: 30,
      speed: 1,
      scores: 0,
      isPlaying: false,
    }
  },
  methods: {
    gameBtn() {
      this.isPlaying = !this.isPlaying
    }
  }
}
</script>

<style scoped>
body {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

h1 {
  text-align: center;
  margin: 3rem 0;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  text-align: center;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  column-gap: 3rem;
}

.col {
  display: flex;
  flex-direction: column;
  border: 1px solid #ccc;
  border-radius: 10px;
  padding: 1rem;
}

.col input {
  margin-top: 1rem;
  padding: 0 5px;
}

.controls {
  grid-column: 2;
  margin: 0 auto;
  display: flex;
  align-items: center;
}

.scores {
  margin-right: 2rem;
}

.play-btn {
  cursor: pointer;
  padding: 0.75rem 0.5rem;
}
</style>
