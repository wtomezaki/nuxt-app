<!-- eslint-disable vue/no-v-html -->
<template>
  <div class="card" :class="{ selected: isSelected }">
    <img :src="user.avatar" class="cardAvatar" />
    <div class="cardContent">
      <div class="cardInfo">
        <div class="cardEmail">
          <p v-html="highlight(user.email)"></p>
        </div>
        <div class="cardTitle">
          <h2 v-html="highlight(user.name)"></h2>
        </div>
        <div class="cardSubtitle">
          <h4 v-html="highlight(user.title)"></h4>
        </div>
        <div class="cardAddress">
          <p v-html="highlight(user.address + ', ' + user.city)"></p>
        </div>
      </div>
      <div class="cardAction">
        <Button
          :text="isSelected ? 'SKIP SELECTION' : 'MARK AS SIUTABLE'"
          @click="$nuxt.$emit('userClicked', user)"
        />
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
    query: { type: String, required: true },
    selected: { type: String, required: true },
  },
  computed: {
    isSelected() {
      return this.selected === this.user.email
    },
  },
  methods: {
    highlight(content: string): string {
      if (!this.query) {
        return content
      }
      return content.replace(new RegExp(this.query, 'gi'), (match) => {
        return '<span class="highlightText">' + match + '</span>'
      })
    },
  },
})
</script>

<style>
h4,
p {
  color: #727272;
}
.card {
  border-radius: 5px;
  height: 120px;
  margin: 15px 0;
  display: flex;
  flex-direction: row;
  background-color: #fafafa;
}
.cardAvatar {
  width: 20%;
  max-width: 300px;
  background-color: #bbbbbb;
  object-fit: contain;
  border-radius: 5px 0 0 5px;
}
.cardContent {
  width: 80%;
  padding: 10px 10px 10px 30px;
  display: flex;
  flex-direction: column;
}
.cardInfo {
  height: 70%;
}
.cardAction {
  border-top: 1px solid #bbbbbb;
  height: 30%;
}
.cardEmail {
  position: relative;
  top: 0;
  float: right;
}
.cardTitle {
  text-overflow: ellipsis;
}
.cardSubtitle {
  margin-bottom: 2px;
}
.highlightText {
  background: yellow;
}
.selected {
  border: 1px solid blue;
}
</style>
