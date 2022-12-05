<script setup>
import ConwayGrid from './components/ConwayGrid.vue';
</script>

<template>
<ConwayGrid />
</template>

<style>
.btn{
  border: 2px solid #3C6E71;
  color: var(--color-orange);
  background-color: var(--color-base-2);
  height: 24px;
}

.btn-selected{
  background-color: #3C6E71;
  color: white;
  border: 2px solid #3C6E71;
}

.btn-deactivated{
  border: 2px solid #D9D9D9;
  color: #D9D9D9;
}

.btn-deactivated-selected{
  border: 2px solid #D9D9D9;
  color: white;
  background-color: #D9D9D9;
}

.options{
  display:flex;
  align-items: center;
  gap: 16px;
}
.main{
  font-family: Arial, sans-serif;
  color: #284B63;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 16px;
  font-weight: bold;
}

.grid-size-selector{
  display: grid;
  grid-template-columns: auto auto;
  grid-gap: 4px;
}

.probability{
  display: flex;
  padding-bottom: 8px;
  justify-content: center;
  text-align: center;
}

.range{
  -webkit-appearance: none;
  width: auto;
  height: 15px;
  background: #D9D9D9;
  outline: none;
  border: 2px solid #3C6E71;
  border-radius: 8px;
  display: block;
}

.range-deactivated{
  -webkit-appearance: none;
  background: #D9D9D9;
  border: 2px solid #D9D9D9;
  pointer-events: none;
}

.text-deactivated{
  color: #D9D9D9;
}

.range::-moz-range-thumb {
  background: #3C6E71;
  cursor: pointer;
}

.range-deactivated::-moz-range-thumb {
  background: #D9D9D9;
  cursor: pointer;
}

.range::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 16px;
  height: 16px;
  border-radius: 50%;
  background: #3C6E71;
  cursor: pointer;
}

.range-deactivated::-webkit-slider-thumb {
  background: #D9D9D9;
}
</style>
