<template>
  <div class="inputSection">
    <div class="addInputSection">
      <input type="text" v-model="newTodoItem" @keyup.enter="addTodo"/>
      <button class="inputBtn" @click="addTodo">add</button>
    </div>
    <TodoList
        :todo-array="todoArray"
        :msg="msg"
        @fnEdit="fnEdit"
        @clearTodo="clearTodo"
        @deleteTodo="deleteTodo"
        @checkTodo="checkTodo"
        @editItem="editItem"
    ></TodoList>
  </div>
</template>

<script>
import TodoList from './TodoList.vue'

export default {
  data () {
    return {
      newTodoItem: '',
      todoArray: [],
      msg: ''
    }
  },
  created () {
    if (this.todoArray.length !== 0) {
      this.todoArray = JSON.parse(localStorage.getItem('todolist'))
    } else if (this.todoArray.length === 0) {
      this.msg = '할일이 없어요.'
    }
  },
  methods: {
    addTodo () {
      if (this.newTodoItem === '') {
        alert('할일을 입력하세요')
      } else {
        const itemArray = this.todoArray.map(todo => todo.item)
        if (itemArray.indexOf(this.newTodoItem) !== -1) {
          alert('이미 등록된 할일입니다.')
          return
        }
        const itemInfo = { item: this.newTodoItem && this.newTodoItem.trim(), isCompleted: false, isEdit: false }
        this.todoArray.push(itemInfo)
        this.newTodoItem = ''
        localStorage.setItem('todolist', JSON.stringify(this.todoArray))
        this.msg = ''
      }
    },
    checkTodo () {
      localStorage.setItem('todolist', JSON.stringify(this.todoArray))
    },
    fnEdit () {
      localStorage.setItem('todolist', JSON.stringify(this.todoArray))
    },
    editItem (editTodoItem, index) {
      this.todoArray = JSON.parse(localStorage.getItem('todolist'))
      this.todoArray[index].item = editTodoItem
      this.todoArray[index].isEdit = false
      localStorage.setItem('todolist', JSON.stringify(this.todoArray))
    },
    deleteTodo (index) {
      this.todoArray = JSON.parse(localStorage.getItem('todolist'))
      this.todoArray.splice(index, 1)
      localStorage.setItem('todolist', JSON.stringify(this.todoArray))
      if (this.todoArray.length === 0) {
        this.msg = '할일이 없어요.'
      }
    },
    clearTodo () {
      localStorage.clear()
      this.msg = '할일이 없어요.'
      this.todoArray = []
    }
  },
  components: {
    TodoList
  }
}
</script>

<style lang="scss">

</style>
