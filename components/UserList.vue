<template>
  <div v-if="users.length" class="userList">
    <div v-for="(user, index) of users" :key="index">
      <Card :user="user" />
    </div>
  </div>
  <div v-else class="noResults"><h1>No results.</h1></div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'UserList',
  props: {
    users: { type: Array, required: true },
  },
})
</script>

<style>
.userList {
  height: calc(95% - 20px);
  overflow-y: auto;
}
.noResults {
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
