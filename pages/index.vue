<template>
  <div class="body">
    <div class="container">
      <div class="searchContainer">
        <input
          v-model="query"
          class="searchInput"
          type="search"
          autocomplete="off"
        />
      </div>

      <div v-if="users.length" class="userList">
        <div v-for="user of users" :key="user.email" class="card">
          <img :src="user.avatar" class="cardAvatar" />
          <div class="cardContent"></div>
          <div class="cardTitle">
            <h2>{{ user.name }}</h2>
          </div>
          <div class="cardEmail">
            <h4>{{ user.email }}</h4>
          </div>
          <div class="cardSubtitle">
            <h4>{{ user.title }}</h4>
          </div>
        </div>
      </div>
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

.searchContainer {
  width: 100%;
  position: relative;
  top: 0;
  height: 5%;
  margin: 10px 0;
}
.searchInput {
  width: 100%;
  height: 100%;
  font-size: 120%;
}

.userList {
  height: 95%;
  overflow-y: auto;
}

.card {
  height: 120px;
  margin: 15px 0;
  display: flex;
  flex-direction: row;
  background-color: rgba(211, 211, 211, 0.5);
}

.cardAvatar {
  width: 20%;
  background-color: lightgray;
  object-fit: contain;
}

.cardContent {
  /* width: 80%; */
  padding: 15px 10px;
}
</style>
