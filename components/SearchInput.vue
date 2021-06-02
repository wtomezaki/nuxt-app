<template>
  <div class="searchContainer">
    <i class="searchIcon"><font-awesome-icon :icon="['fas', 'search']" /></i>
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
    query: { type: String, default: '' },
  },
  computed: {
    listeners() {
      return {
        ...this.$listeners,
        input: (event: any): void => this.$emit('input', event.target.value),
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
  background-color: #fafafa;
  box-shadow: 1px 2px #c9c9c9;
  border: none;
  width: 100%;
  padding: 8px 10px 8px 35px;
  font-size: 120%;
}
.searchIcon {
  position: absolute;
  left: 10px;
  top: 9px;
}
</style>
