<template>
  <div>
    <TodoHeader/>
    <TodoInput
        @addTodo="addTodo"/>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'

export default {
  name: 'App',
  data () {
    return {
      todoList: []
    }
  },
  created () {

  },
  methods: {
    addTodo (todoArray, itemArray) {
      this.todoList = todoArray
      console.log(todoArray)
      console.log(this.todoList)
      console.log(itemArray)
    }
  },
  components: {
    TodoHeader,
    TodoInput
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
