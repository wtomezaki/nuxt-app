<template>
  <button class="button" @click="$emit('click', undefined)">
    {{ text.toUpperCase() }}
  </button>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'Button',
  props: {
    text: { type: String, required: true },
  },
})
</script>

<style>
.button {
  padding: 5px 10px;
  border: none;
  max-width: 64px;
  background-color: transparent;
  color: #1fa296;
  font-size: 1.2em;
  font-weight: bold;
  text-align: center;
}
</style>
