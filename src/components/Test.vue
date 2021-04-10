<template>
  <div class="container test">
    <a href="/">跳转HelloWorld</a>
    <br>
    <h1>{{ msg }}</h1>
    <button @click="add">Add</button>
    <button @click="remove">Remove</button>
    <transition-group name="list" tag="p">
      <span v-for="item in items" :key="item" class="list-item">{{ item }}</span>
    </transition-group>

    <p>{{ msg2 }}</p>
    <input v-model.lazy="msg2" placeholder="在文本框中输入文字..."/>
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
    <input type="radio" value="female" v-model="picked"/>female
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
    <alert-box></alert-box>
    <alert-box>something error msg</alert-box>
    <br>
    <todo-list>
      <template v-slot:todo-list="slotProps">
        <span style="font-size: 1.5em">{{ slotProps.item }}</span>
      </template>
    </todo-list>
    <br>
    <!--缩写-->
    <todo-list #todo-list="slotProps">
      <span style="font-size: 1.5em">{{ slotProps.item }}</span>
    </todo-list>
    <br>
    <!--    bus总线通信    -->
    <child1></child1>
    <child2></child2>
    <br>

  </div>
</template>

<script>
import Vue from 'vue'

const componentA = Vue.component('alert-box', {
  name: 'alert-box',
  template: `
          <div id="alert-box"   style="background-color: gold">
          <strong>Error: </strong>
          <slot></slot>
          <slot name="alert-box">default text</slot>
          </div>
        `
})
const componentB = Vue.component('todo-list', {
  name: 'todo-list',
  data () {
    return {
      items: ['Feed a cat', 'Buy milk', 'Jack love Rose']
    }
  },
  template: `
    <ul>
    <li v-for="(item, index) in items">
      {{ index }}-
      <slot name="todo-list" :item="item"></slot>
    </li>
    </ul>
  `
})

const bus = new Vue() /* bus */
const child1 = Vue.component('child1', {
  name: 'child1',
  template: `
    <div id="child1">
    child1:
    <button @click="handleClick">发送信息</button>
    </div>
  `,
  methods: {
    handleClick: function () {
      bus.$emit('sendmsg', 'msg child1 send to child2')
    }
  }
})
const child2 = Vue.component('child2', {
  name: 'child2',
  template: `
    <div id="child2">
    child2:
    <transition name="fade" :duration="{ enter: 500, leave: 800 }" mode="out-in">
      <p v-if="msg != ''">{{ msg }}</p>
    </transition>
    </div>
  `,
  data () {
    return {
      msg: ''
    }
  },
  mounted () {
    bus.$on('sendmsg', (data) => {
      console.log(data)
      this.msg = data
    })
  }
})
export default {
  name: 'Test',
  components:
    {
      'alert-box': componentA,
      'todo-list': componentB,
      'child1': child1,
      'child2': child2
    },
  props: {
    msg: {
      type: String,
      default: 'This is Test.vue'
    }
  },
  data () {
    return {
      items: [1, 2, 3, 4, 5, 6, 7, 8, 9],
      nextNum: 10,
      msg1: 'textarea',
      msg2: 'input',
      checked: false,
      checkedNames: [],
      picked: '',
      selected: '',
      selected1: []
    }
  },
  methods: {
    randomIndex () {
      return Math.floor(Math.random() * this.items.length)
    },
    add () {
      this.items.splice(this.randomIndex(), 0, this.nextNum++)
    },
    remove () {
      this.items.splice(this.randomIndex(), 1)
    }
  }
}
</script>

<style scoped>
.test {
  display: inline-block;
  margin-right: 10px;
}

.list-enter-active,
.list-leave-active {
  transition: all 1s ease;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>
