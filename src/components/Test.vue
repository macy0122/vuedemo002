<template>
  <div class="container test">
    <!--    <h1>This is Test.vue</h1>-->
    <h1>{{ msg }}</h1>
  </div>
</template>

<script>
export default {
  name: 'Test',
  props: {
    msg: {
      type: String,
      default: 'This is Test.vue'
    }
  }
}
</script>

<style scoped>
.test {
  border: dodgerblue 1px solid;
}
</style>
