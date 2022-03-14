<template>
  <div>
    <div class="container">
    <form>
      <input v-model="searchChar" type="text">
      <NuxtLink :to="{name: 'result', query: {searchChar: searchChar}}">
        <button>search</button>
      </NuxtLink>
    </form>
    </div>
    <br>
  </div>
</template>

<script>
import Vue from 'vue'

export default Vue.extend({
  name: 'IndexPage',
  data(){
    const searchChar = ''
    return {
      searchChar
    }
  }
})
</script>

<style scoped>
.container{
  width: 15rem;
  height: 1rem;
  margin: 0 auto;
  padding: 1rem;
}
</style>