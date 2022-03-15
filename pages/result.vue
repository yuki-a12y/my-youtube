<template>
  <div>
    <searchInput />
    <div v-for="item in youtubeData" :key="item.id.videoId">
      <NuxtLink :to="{name: 'watchVideo', query: {videoId: item.id.videoId }}">
        <div class="result-container">
          <p>{{ item.snippet.title }}</p>
          <p>{{ item.snippet.channelTitle }}</p>
        </div>
      </NuxtLink>
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
          key: this.$config.apiKey,
          type: 'video',
          part: 'snippet',
          q: to.query.searchChar
        }
      })
      .then((res) => {
        this.youtubeData = res.data.items
      })
      .catch(function(err) {
        console.log(err);
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
      .catch(function(err) {
        console.log(err);
      })
  }
})
</script>

<style scoped>
.result-container{
  border-bottom: solid 0.1rem rgb(100 100 100);
}

.result-container p{
  color: rgb(40 40 40);
}
</style>