<template>
  <div class="searchContainer">
    <input
      class="searchInput"
      type="search"
      autocomplete="off"
      placeholder="Search"
      v-on="listeners"
    />
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'SearchInput',
  props: {
    query: { type: String, required: true },
  },
  computed: {
    listeners() {
      return {
        // Pass all component listeners directly to input
        ...this.$listeners,
        // Override input listener to work with v-model
        input: (event) => this.$emit('input', event.target.value),
      }
    },
  },
})
</script>

<style>
.searchContainer {
  width: 100%;
  position: relative;
  top: 0;
  height: 5%;
  margin: 10px 0;
}
.searchInput {
  width: 100%;
  padding: 8px 10px;
  font-size: 120%;
}
</style>
