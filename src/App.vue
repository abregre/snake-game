<template>
  <h1 class="page-title">Snake Game</h1>
  <info-message
    v-if="showMessage"
    :username="username"
    :score="scores"
    :play-again="play"
  ></info-message>
  <div class="container">
    <snake-canvas
      :cellSize="cellSize"
      :boardSize="boardSize"
      :speed="speed"
      :isPlaying="isPlaying"
      :stop="stop"
      :score="scores"
      :add-score="addScore"
      :speed-increase="speedIncrease"
    />
    <div class="controls">
      <div class="form-control">
        <label>Username</label>
        <input type="text" v-model="username" />
      </div>
      <div class="scores">Scores: {{ scores }}</div>
      <button class="play-btn" v-on="playStop">
        {{ isPlaying ? 'Stop' : 'Play' }}
      </button>
    </div>
  </div>
  <div class="container">
    <rankings></rankings>
  </div>
</template>

<script>
import InfoMessage from './components/InfoMessage.vue'
import Rankings from './components/Rankings.vue'
import SnakeCanvas from './components/SnakeCanvas.vue'
export default {
  name: 'App',
  components: { SnakeCanvas, InfoMessage, Rankings },
  data() {
    return {
      cellSize: 20,
      boardSize: 30,
      speed: 10,
      scores: 0,
      isPlaying: false,
      showMessage: false,
      username: '',
      rankingsList: []
    }
  },
  computed: {
    playStop() {
      if (this.isPlaying) {
        return { click: this.stop }
      }
      return { click: this.play }
    },
  },
  methods: {
    play() {
      this.isPlaying = true
      this.scores = 0
      this.showMessage = false
    },
    stop() {
      this.isPlaying = false
      this.showMessage = true
      setTimeout(() => (this.showMessage = false), 3000)
    },
    speedIncrease(newSpeed) {
      this.speed += newSpeed
    },
    addScore(score) {
      this.scores += score
    },
  },
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Ubuntu&display=swap');

body {
  height: 100vh;
  font-family: 'Ubuntu', sans-serif;
}

.page-title {
  text-align: center;
  margin: 3rem 0;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  text-align: center;
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
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: center;
}
.form-control {
  display: flex;
  flex-direction: column;
  margin-left: 2rem;
}

.scores {
  margin-left: 2rem;
}

.play-btn {
  cursor: pointer;
  padding: 0.75rem 0.5rem;
  margin-left: 2rem;
}
</style>
