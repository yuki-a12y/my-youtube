<template>
  <div>
    <input v-model="searchChar">
    <NuxtLink :to="{name: 'result', query: {searchChar: searchChar}}">
      <button>search</button>
    </NuxtLink>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'IndexPage',
  data(){
    const searchChar: string = ''
    return {
      searchChar
    }
  }
})
</script>
