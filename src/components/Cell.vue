<script>
export default {
  props: {
    x: Number,
    y: Number, 
    isAlive: Boolean
  }
}
</script>

<template>
  <span class="cell" :class="{ alive: isAlive }"></span> 
</template>

<style>
.cell {
  padding: 7px;
  margin: 1px;
  border: 2px solid #3C6E71;
}

.alive {
  background-color: #284B63;
}
</style>
