<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <a href="/test">跳转test</a>
    <br>
<!--    <Test msg="hello"></Test>-->
  </div>
</template>

<script>

// import Test from './Test'

export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
  // ,
  // components: {
  //   'Test': Test
  // }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  font-weight: normal;
}
</style>
