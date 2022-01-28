<template>
  <div>
    <TodoHeader/>
    <TodoInput
        :todoList="todoList"
    />
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
