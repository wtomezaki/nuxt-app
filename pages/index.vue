<template>
  <div class="body">
    <div class="container">
      <SearchInput v-model="query" />
      <UserList :users="users" :query="query" :selected="selected" />
    </div>
  </div>
</template>

<script lang="ts">
import { IContentDocument } from '@nuxt/content/types/content'
import Vue from 'vue'

interface User {
  name: string
  email: string
  title: string
  city: string
  address: string
  avatar: string
}

export default Vue.extend({
  data(): {
    query: string
    users: IContentDocument | IContentDocument[]
    selected?: string
  } {
    return {
      query: '',
      users: [],
      selected: '',
    }
  },
  watch: {
    async query(query) {
      this.users = await this.getContent().search(query).fetch()
    },
  },
  async mounted(): Promise<void> {
    this.users = await this.getContent()
      .search(this.$route.params.query || '')
      .fetch()
  },
  created(): void {
    this.$nuxt.$on('userClicked', (user: User) => {
      if (this.selected === user?.email) {
        this.selected = ''
      } else {
        this.selected = user.email
      }
    })
  },
  beforeDestroy() {
    this.$nuxt.$off('userClicked')
  },
  methods: {
    getContent() {
      return this.$content('').limit(20).sortBy('name', 'asc')
    },
  },
})
</script>

<style>
.body {
  background-color: #eeeeee;
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
  height: 100vh;
  width: 100%;
}
@media only screen and (min-width: 600px) {
  .container {
    width: 90%;
    height: 90vh;
  }
}
@media only screen and (min-width: 768px) {
  .container {
    width: 80%;
    height: 85vh;
  }
}
@media only screen and (min-width: 992px) {
  .container {
    width: 70%;
    height: 80vh;
  }
}
@media only screen and (min-width: 1200px) {
  .container {
    width: 65%;
  }
}
@media only screen and (min-width: 1920px) {
  .container {
    width: 40%;
  }
}
</style>
