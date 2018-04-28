<template>
  <div class="home">
    <h1>Simple Movie ReVue Search</h1>
    <img src="../assets/logo.png">

    <!-- This is where the HelloWorld component is injected -->
    <ReviewSearch msgParm="Welcome to ReVue Search"/>

  </div>
</template>

<script>
// @ is an alias to /src
import ReviewSearch from '@/components/ReviewSearch.vue'

export default {
  name: 'home',
  components: {
    ReviewSearch
  }
}
</script>
