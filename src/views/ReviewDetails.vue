<template>
  <div class="reviewDetails">
    <h1>REVIEW DETAILS</h1>
    <p>
      Detail data here: {{ bla }}
    </p>
  </div>
</template>

<script>
export default {
  name: 'ReviewDetails',
  props: {
    bla: String
  },
  methods: {
    goBack() {
      console.log("GOBACK");
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 p {
  color: red;
}
</style>
