<script>
export default {
  methods:{
    changedProb(prob) {
      if (!this.running) {
        this.current_prob = prob.target.value
        this.$emit('set-prob', prob.target.value)
      }
    }
  },
  
  data() {
    return {
      current_prob: 5
    }
  },
  
  props: ['size', 'running']
}
</script>

<template>
<div class="options">
  <div class="grid-size-selector">
    <button 
      class="btn" 
      @click="$emit('set-size', 5)"
      :class="{ 'btn-selected': this.size == 5, 'btn-deactivated': this.running }">5X5</button>
    <button 
      class="btn" 
      @click="$emit('set-size', 10)"
      :class="{ 'btn-selected': this.size == 10, 'btn-deactivated': this.running }">10x10</button>
    <button 
      class="btn" 
      @click="$emit('set-size', 20)"
      :class="{ 'btn-selected': this.size == 20, 'btn-deactivated': this.running }">20x20</button>
    <button 
      class="btn" 
      @click="$emit('set-size', 50)"
      :class="{ 'btn-selected': this.size == 50, 'btn-deactivated': this.running }">50x50</button>
  </div>

  <form 
    class="probability">
    <div>
      <span :class="{ 'text-deactivated': this.running }">Probability: 0.{{current_prob}}</span>
      <input 
        class="range" 
        id="prob-slider" 
        max="10" 
        min="0" 
        name="slider" 
        type="range" 
        :value="current_prob"
        @change="changedProb"
        :disabled="running"
        :class="{ 'range-deactivated': this.running }">
    </div>
  </form>
  
  <button 
    class="btn" 
    @click="$emit('randomize-grid')"
    :class="{ 'btn-deactivated': this.running }">Randomize</button>   
</div>
</template>

<style>

</style>
