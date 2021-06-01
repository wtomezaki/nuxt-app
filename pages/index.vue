<template>
  <div>
    <input v-model="query" type="search" autocomplete="off" />

    <ul v-if="users.length">
      <li v-for="user of users" :key="user.email">
        <div>{{ user.name }}</div>
        <div>{{ user.email }}</div>
        <div>{{ user.title }}</div>
      </li>
    </ul>
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
      this.users = await this.$content('').limit(10).search(query).fetch()
    },
  },
  async mounted(): Promise<void> {
    this.users = await this.$content('').limit(10).fetch()
  },
})
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
