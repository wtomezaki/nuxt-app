<template>
  <div class="body">
    <div class="container">
      <SearchInput v-model="query" />

      <div v-if="users.length" class="userList">
        <div v-for="(user, index) of users" :key="index">
          <Card :user="user" />
        </div>
      </div>
      <div v-else class="noResults"><h1>No results.</h1></div>
    </div>
  </div>
</template>

<script lang="ts">
import { IContentDocument } from '@nuxt/content/types/content'
import Vue from 'vue'

export default Vue.extend({
  data(): { query: string; users: IContentDocument | IContentDocument[] } {
    return {
      query: '',
      users: [],
    }
  },
  watch: {
    async query(query) {
      this.users = await this.$content('').limit(20).search(query).fetch()
    },
  },
  async mounted(): Promise<void> {
    this.users = await this.$content('').limit(20).fetch()
  },
})
</script>

<style>
.body {
  background-color: aliceblue;
  padding: 10px 0;
  min-height: 100vh;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.container {
  background-color: white;
  padding: 16px 32px;
  height: 80vh;
  width: 40%;
}
.userList {
  height: 95%;
  overflow-y: auto;
}
.noResults {
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
