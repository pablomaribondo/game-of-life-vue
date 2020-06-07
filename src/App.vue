<template>
  <div>
    <h1>The Game of Life</h1>
    <Buttons
      @play="play"
      @pause="pause"
      @clear="clear"
      @slow="slow"
      @fast="fast"
      @seed="seed"
      @gridSize="gridSize"
      :state="gameState"
    />
    <Grid
      :fullGrid="fullGrid"
      :cols="cols"
      :rows="rows"
      @selectBox="selectBox"
    />
    <h2>Generations: {{ generation }}</h2>
  </div>
</template>

<script>
import Buttons from '@/components/Buttons.vue';
import Grid from '@/components/Grid.vue';

export default {
  name: 'App',
  components: {
    Buttons,
    Grid,
  },

  data() {
    return {
      speed: 100,
      rows: 30,
      cols: 50,
      generation: 0,
      fullGrid: [],
      ticker: undefined,
      gameState: 'stopped',
    };
  },

  created() {
    this.seed();
  },

  methods: {
    selectBox({ row, col }) {
      const gridCopy = [...this.fullGrid];
      gridCopy[row][col] = !gridCopy[row][col];
      this.fullGrid = gridCopy;
    },
    play() {
      if (this.gameState !== 'running') {
        this.ticker = setInterval(() => {
          const gridCopy = [...this.fullGrid];

          for (let i = 0; i < this.rows; i += 1) {
            for (let j = 0; j < this.cols; j += 1) {
              let count = 0;
              if (i > 0) {
                if (this.fullGrid[i - 1][j]) count += 1;
              }
              if (i > 0 && j > 0) {
                if (this.fullGrid[i - 1][j - 1]) count += 1;
              }
              if (i > 0 && j < this.cols - 1) {
                if (this.fullGrid[i - 1][j + 1]) count += 1;
              }
              if (j < this.cols - 1) {
                if (this.fullGrid[i][j + 1]) count += 1;
              }
              if (j > 0) {
                if (this.fullGrid[i][j - 1]) count += 1;
              }
              if (i < this.rows - 1) {
                if (this.fullGrid[i + 1][j]) count += 1;
              }
              if (i < this.rows - 1 && j > 0) {
                if (this.fullGrid[i + 1][j - 1]) count += 1;
              }
              if (i < this.rows - 1 && j < this.cols - 1) {
                if (this.fullGrid[i + 1][j + 1]) count += 1;
              }
              if (this.fullGrid[i][j] && (count < 2 || count > 3)) { gridCopy[i][j] = false; }
              if (!this.fullGrid[i][j] && count === 3) { gridCopy[i][j] = true; }
            }
          }

          this.fullGrid = gridCopy;
          this.generation += 1;
        }, this.speed);

        this.gameState = 'running';
      }
    },
    pause() {
      clearInterval(this.ticker);
      this.gameState = 'paused';
    },
    slow() {
      this.pause();
      this.speed = 1000;
      this.play();
    },
    fast() {
      this.pause();
      this.speed = 100;
      this.play();
    },
    clear() {
      clearInterval(this.ticker);
      this.fullGrid = this.clearGrid();
      this.generation = 0;
      this.gameState = 'stopped';
    },
    clearGrid() {
      return Array(this.rows).fill().map(() => Array(this.cols).fill(false));
    },
    gridSize(event) {
      const sizeArray = event.split('x');
      this.cols = parseInt(sizeArray[0], 10);
      this.rows = parseInt(sizeArray[1], 10);
      this.seed();
    },
    seed() {
      const gridCopy = this.clearGrid();

      for (let i = 0; i < this.rows; i += 1) {
        for (let j = 0; j < this.cols; j += 1) {
          if (Math.floor(Math.random() * 5) === 1) {
            gridCopy[i][j] = true;
          }
        }
      }

      this.fullGrid = gridCopy;
    },
  },
};
</script>

<style lang="scss">
body {
  background-image: url(http://subtlepatterns2015.subtlepatterns.netdna-cdn.com/patterns/pink%20dust.png);
}

h1, h2, h3, h4 {
  color: #fff;
  margin: auto;
  text-align: center;
  width: 50%;
  margin-top: 10px !important;
}

h4 {
  margin-top: 0px;
}
</style>
