<template>
  <button type="button" class="button" @click="$emit('click')">
    {{ text }}
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
  background-color: transparent;
  color: #1fa296;
  font-size: 1.05em;
  font-weight: 600;
  text-align: center;
}
</style>
