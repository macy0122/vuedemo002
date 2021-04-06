<template>
  <div id="app">
    <!--    <img src="./assets/logo.png">-->
    <router-view name="default"/>
    <p>{{ msg }}</p>
    <input v-model.lazy="msg" placeholder="在文本框中输入文字..."/>
    <br>
    <p>{{ msg1 }}</p>
    <textarea v-model.trim="msg1" placeholder="在多行文本框中输入文字..."/>
    <br>
    <span>单个复选框:</span><br>
    <input type="checkbox" id="checkbox" v-model="checked"/>
    <label for="checkbox">checked: {{ checked }}</label>
    <br>
    <span>多个复选框:</span><br>
    <input type="checkbox" id="jack" value="Jack" v-model="checkedNames"/>
    <label for="jack">Jack</label>
    <input type="checkbox" id="john" value="John" v-model="checkedNames"/>
    <label for="john">John</label>
    <input type="checkbox" id="mike" value="Mike" v-model="checkedNames"/>
    <label for="mike">Mike</label>
    <br/>
    <span>Checked names: {{ checkedNames }}</span>
    <br>
    <span>单选框:</span><br>
    <input type="radio" value="man" v-model="picked"/>man
    <input type="radio" value="femanl" v-model="picked"/>femanl
    <br>
    <span>picked : {{ picked }}</span>
    <br>
    <select v-model="selected">
      <option disabled="disabled" value="">Please select one</option>
      <option>A</option>
      <option>B</option>
      <option>C</option>
    </select>
    <br>
    <span>selected : {{ selected }}</span>
    <br>
    <select v-model="selected1" multiple>
      <option disabled="disabled" value="">Please select one</option>
      <option>A</option>
      <option>B</option>
      <option>C</option>
      <option>D</option>
      <option>E</option>
    </select>
    <br>
    <span>selected : {{ selected1 }}</span>
    <br>
    <br>
    <alert-box>
      something error msg
    </alert-box>
    <br>
    <label>my-component v-model:foo="bar" </label>
<!--    <my-component v-model:foo="bar"></my-component>-->
  </div>
</template>

<script>

import Vue from 'vue'

const componetA = Vue.component('alert-box', {
  name: 'alert-box',
  template: `
          <div id="alert-box"   style="background-color: gold">
          <strong>Error: </strong>
          <slot></slot>
          </div>
        `
})
// const componetB = Vue.component('my-component', {
//   props: {
//     foo: String,
//     default: 'aa'
//   },
//   template: `
//     <input
//       type="text"
//       :value="foo"
//       @input="$emit('update:foo', $event.target.value)"/>
//   `
// })
export default {
  name: 'App',
  components: [
    {
      'alert-box': componetA
      // componetB
    }
  ],
  data () {
    return {
      msg: 'input',
      msg1: 'textarea',
      checked: false,
      checkedNames: [],
      picked: '',
      selected: '',
      selected1: []
    }
  },
  methods: {}
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
