<template>
  <div>
    <searchInput />
    <youtube
    ref="youtube"
    :video-id="videoId"/>
  </div>
</template>

<script>
import Vue from 'vue'
import VueYoutube from 'vue-youtube'

Vue.use(VueYoutube)

export default Vue.extend({
    data(){
        const videoId = this.$route.query.videoId
        return {
            videoId
        }
    }
})
</script>