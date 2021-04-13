<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <a href="/test">跳转test</a>
    <br>
    <Test1/>
  </div>
</template>

<script>

import Test1 from './Test1'
// import {reactive, ref} from 'vue'

export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  components: {
    'Test1': Test1
  },
  // setup () {
  //   const todo = ref('todo something ref')
  //   const user = reactive({
  //     name: 'Jack reactive',
  //     age: 20
  //   })
  //
  //   this.provide('todo', todo)
  //   this.provide('user', user)
  // }

  // provide/inject 提供/注入
  provide: {
    todo: 'todo something',
    user: {
      name: 'Jack',
      age: 20
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  font-weight: normal;
}
</style>
