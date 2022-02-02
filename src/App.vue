<template>
  <div id ="app">
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

<style lang="scss">
@font-face {
  font-family: 'SANGJUDajungdagam';
  src: url('https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts_2112@1.0/SANGJUDajungdagam.woff') format('woff');
  font-weight: normal;
  font-style: normal;
}

#app {
  font-family: SANGJUDajungdagam, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
