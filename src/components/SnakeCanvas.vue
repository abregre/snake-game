<template>
  <canvas
    ref="board"
    id="snake-canvas"
    :width="boardSizePx"
    :height="boardSizePx"
  />
</template>

<script>
export default {
  name: 'SnakeCanvas',
  props: {
    cellSize: Number,
    boardSize: Number,
    speed: Number,
    isPlaying: Boolean,
  },
  mounted() {
    this.boardContext = this.$refs.board.getContext('2d')
  },
  created() {
    this.resetSnake()
  },
  computed: {
    boardSizePx() {
      return this.cellSize * this.boardSize
    },
  },
  watch: {
      isPlaying(val) {
          if(val) {
              this.resetSnake()
              this.move()
          }
      }
  },
  methods: {
    resetSnake() {
      this.snake = [
        {
          x: this.getMiddleCell(),
          y: this.getMiddleCell(),
        },
      ]
    },
    getMiddleCell() {
      return Math.round(this.boardSize / 2)
    },
    move() {
        this.snake.forEach(this.drawCell)
    },
    drawCell({ x, y }) {
      this.boardContext.rect(
        x * this.cellSize,
        y * this.cellSize,
        this.cellSize,
        this.cellSize
      )
      this.boardContext.fillStyle = 'black'
      this.boardContext.fill()
    },
    getMoveDelay(){
        return 2/this.speed*1000
    }
  },
}
</script>

<style scoped>
#snake-canvas {
  border: 1px solid #ccc;
  border-radius: 10px;
  margin: 2rem auto;
  grid-column: 2;
}
</style>
