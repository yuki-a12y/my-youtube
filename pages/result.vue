<template>
  <div>
    <input v-model="searcChar">
    <NuxtLink :to="{name: 'result', query: {searcChar: searcChar}}">
      <button>search</button>
    </NuxtLink>
    <div v-for="item in youtubeData" :key="item.id.videoId">
      <NuxtLink :to="{name: 'watchVideo', query: {videoId: item.id.videoId }}">{{ item.snippet.title }}</NuxtLink>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'IndexPage',
    beforeRouteUpdate (to, _from, next){
    next()
    this.$axios.get('https://www.googleapis.com/youtube/v3/search', {
        params: {
        key: 'AIzaSyD2gn2eMBuv8ofuNv_H9ckzf985y6GBLrU',
        type: 'video',
        part: 'snippet',
        q: to.query.searcChar
        }
      })
      .then((res) => {
        this.youtubeData = res.data.items
      })
  },
  data(){
    const searcChar: string = '';
    const youtubeData: Array<5> = [];
    return {
      searcChar,
      youtubeData
    }
  },
  mounted (){
    this.$axios.get('https://www.googleapis.com/youtube/v3/search', {
        params: {
        key: 'AIzaSyD2gn2eMBuv8ofuNv_H9ckzf985y6GBLrU',
        type: 'video',
        part: 'snippet',
        q: this.$route.query.searcChar
        }
      })
      .then((res) => {
        this.youtubeData = res.data.items
      })
  }
})
</script>