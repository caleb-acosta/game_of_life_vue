<script>
import Cell from './Cell.vue';
import OptionsPanel from './OptionsPanel.vue';

export default {
  components: {
    Cell,
    OptionsPanel
  }, 

  data() {
    return {
      size: 10,
      interval: null,
      running: false,
      prob: 5,
      grid: []
    }
  },

  methods: {
    randomizeGrid() {
      if (!this.running) { 
        this.grid = [];
        for (let row = 0; row < this.size; row++) {
          this.grid[row] = [];
          for (let cell = 0; cell < this.size; cell++) {
            this.grid[row][cell] = Math.random() < this.prob * 0.1;
          }
        }
      }
    },
    
    toggleCell(x, y) {
      this.grid[y][x] = !this.grid[y][x];
    },

    resetGrid() {
      this.grid = [];
      for (let row = 0; row < this.size; row++) {
        this.grid[row] = [];
        for (let cell = 0; cell < this.size; cell++) {
          this.grid[row][cell] = false;
        }
      }
    },

    aliveNeighbours(x, y) {
      let count = 0;
      for(let row = y - 1; row <= y + 1; row++) {
        for (let col = x - 1; col <= x + 1; col++) {
          // TODO: Optimize this
          if ((row >= 0 && row < this.size) && (col >= 0 && col < this.size))
            if ((x != col || y != row) && this.grid[row][col]) {
            count ++;
          }
        }
      }
      return count;
    },

    nextState() {
      let next_grid = [];
      for (let row = 0; row < this.size; row++) {
         next_grid[row] = [];
        for (let col = 0; col < this.size; col++) {
          let alive_n = this.aliveNeighbours(col, row);
          if (this.grid[row][col] && (alive_n == 2 || alive_n == 3)) {
            next_grid[row][col] = true;
          }
          else if (!this.grid[row][col] && alive_n == 3) {
            next_grid[row][col] = true;
          }
          else {
            next_grid[row][col] = false;
          }
        } 
      }
      this.grid = next_grid;
    },

    toggleRun() {
      if (this.running) {
        clearInterval(this.interval);
        this.running = false;
      }
      else {
        this.interval = setInterval(this.nextState, 500);
        this.running = true;
      }
    },

    setSize(new_size) { 
      if ([5, 10, 20, 50].includes(new_size) && !this.running){
        this.size = new_size;
        this.resetGrid();
      }
    },

    setProb(value) {
      this.prob = value
    }
  },

  created() {
    this.resetGrid() 
  }
}
</script>

<template>
<div class="main">
  <div class="panel">
    <OptionsPanel 
      @set-size="setSize" 
      @set-prob="setProb" 
      @randomize-grid="randomizeGrid"
      :size="size"
      :running="running"/>
    <button @click="toggleRun" class="btn" :class="{ 'btn-selected': running }">{{ running ? 'Stop' : 'Play'}}</button>
  </div>

  <div class="grid-wrapper">
    <div v-for="(row, y) in grid" :key="y" class="row">
        <Cell v-for="(cell, x) in row" :x="x" :y="y" :isAlive="cell" @click="toggleCell(x, y)"></Cell> 
    </div>
  </div>
</div>
</template>

<style>
.row {
  display: flex;
  flex-direction: row;
}

.main {
  display: flex; 
}

.panel {
  display: flex;
  justify-content: center;
  flex-direction: column;
  gap: 10px;
}
</style>
