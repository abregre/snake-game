<template>
  <canvas
    ref="board"
    id="snake-canvas"
    :width="boardSizePx"
    :height="boardSizePx"
  />
</template>

<script>
import constants from './constants.js'

export default {
  name: 'SnakeCanvas',
  props: {
    cellSize: Number,
    boardSize: Number,
    speed: Number,
    isPlaying: Boolean,
    score: Number,
    stop: Function,
    addScore: Function,
    speedIncrease: Function,
  },
  mounted() {
    this.boardContext = this.$refs.board.getContext('2d')
    window.addEventListener('keydown', this.onKeyPress)
  },
  created() {
    this.resetSnake()
  },
  beforeUnmount() {
    window.removeEventListener('keydown', this.onKeyPress)
  },
  computed: {
    boardSizePx() {
      return this.cellSize * this.boardSize
    },
  },
  watch: {
    isPlaying(val) {
      this.clear()
      if (val) {
        this.resetSnake()
        this.move()
      }
    },
  },
  methods: {
    resetSnake() {
      this.snake = [
        {
          x: this.getMiddleCell(),
          y: this.getMiddleCell(),
        },
      ]
      const randomDirection = Math.floor(Math.random()*4)
      this.direction = constants[randomDirection]
      this.targetCell = null
    },
    getMiddleCell() {
      return Math.round(this.boardSize / 2)
    },
    move() {
      if (!this.isPlaying) {
        return
      }
      this.clear()
      this.setTargetCell()
      const newHeadCell = {
        x: this.snake[0].x + this.direction.move.x,
        y: this.snake[0].y + this.direction.move.y,
      }

      if (
        this.borderCollision(newHeadCell) ||
        this.cellsAmountInSnake(this.snake[0]) > 1
      ) {
        this.stop()
      }

      if (this.isTargetNewHead()) {
        this.snake.unshift(this.targetCell)
        this.targetCell = null
        this.speedIncrease(1)
        this.addScore(this.speed)
      } else {
        this.snake.unshift(newHeadCell)
        this.snake.pop()
      }

      this.boardContext.beginPath()
      this.snake.forEach(this.drawCell)
      this.boardContext.closePath()

      setTimeout(this.move, this.getMoveDelay())
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
    clear() {
      this.boardContext.clearRect(0, 0, this.boardSizePx, this.boardSizePx)
    },
    getMoveDelay() {
      return (2 / this.speed) * 1000
    },
    borderCollision({ x, y }) {
      return x < 0 || y < 0 || x >= this.boardSize || y >= this.boardSize
    },
    onKeyPress(e) {
      const newDirection = constants.find((key) => key.keyCode === e.keyCode)

      if (!newDirection) {
        return
      }
      if (Math.abs(newDirection.keyCode - this.direction.keyCode) !== 2) {
        this.direction = newDirection
      }
    },
    setTargetCell() {
      if (!this.targetCell) {
        let targetCell = this.getRandomCell()

        while (this.cellsAmountInSnake(targetCell) > 0) {
          targetCell = this.getRandomCell()
        }
        this.targetCell = targetCell
      }
      this.boardContext.beginPath()
      this.boardContext.rect(
        this.targetCell.x * this.cellSize,
        this.targetCell.y * this.cellSize,
        this.cellSize,
        this.cellSize
      )
      this.boardContext.fillStyle = 'red'
      this.boardContext.fill()
      this.boardContext.closePath
    },
    getRandomCell() {
      return {
        x: Math.floor(Math.random() * this.boardSize),
        y: Math.floor(Math.random() * this.boardSize),
      }
    },
    cellsAmountInSnake(cell) {
      return this.snake.filter(({x, y}) => x === cell.x && y === cell.y).length
    },
    isTargetNewHead() {
      return (
        this.snake[0].x + this.direction.move.x === this.targetCell.x &&
        this.snake[0].y + this.direction.move.y === this.targetCell.y
      )
    },
  },
}
</script>

<style scoped>
#snake-canvas {
  border: 1px solid #ccc;
  margin: 2rem auto;
  grid-column: 2;
}
</style>
