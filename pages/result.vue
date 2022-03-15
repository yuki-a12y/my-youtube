<template>
  <div>
    <searchInput />
    <div v-for="item in youtubeData" :key="item.id.videoId">
      <NuxtLink :to="{name: 'watchVideo', query: {videoId: item.id.videoId }}">{{ item.snippet.title }}</NuxtLink>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'

export default Vue.extend({
  name: 'IndexPage',
    beforeRouteUpdate (to, _from, next){
    next()
    this.$axios.get('https://www.googleapis.com/youtube/v3/search', {
        params: {
        key: 'AIzaSyCbVx8EF4e1jyommmEqjodKg5prVeBuid8',
        type: 'video',
        part: 'snippet',
        q: to.query.searchChar
        }
      })
      .then((res) => {
        this.youtubeData = res.data.items
      })
  },
  data(){
    const youtubeData = [];
    return {
      youtubeData
    }
  },
  mounted (){
    this.$axios.get('https://www.googleapis.com/youtube/v3/search', {
        params: {
        key: this.$config.apiKey,
        type: 'video',
        part: 'snippet',
        q: this.$route.query.searchChar
        }
      })
      .then((res) => {
        this.youtubeData = res.data.items
      })
  }
})
</script>