<template>
  <div class="card">
    <img :src="user.avatar" class="cardAvatar" />
    <div class="cardContent">
      <div class="cardTitle">
        <h2>{{ user.name }}</h2>
      </div>
      <div class="cardSubtitle">
        <h4>{{ user.title }}</h4>
      </div>
      <div class="cardAddress">
        <p>{{ user.address }}, {{ user.city }}</p>
      </div>
      <div class="cardEmail">
        <p>{{ user.email }}</p>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'Card',
  props: {
    user: { type: Object, required: true },
  },
})
</script>

<style>
.card {
  height: 120px;
  margin: 15px 0;
  display: flex;
  flex-direction: row;
  background-color: #fafafa;
}

.cardAvatar {
  width: 20%;
  background-color: #bbbbbb;
  object-fit: contain;
}

.cardContent {
  /* width: 80%; */
  padding: 15px 10px;
}
</style>
