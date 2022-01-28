<template>
  <div>
    <div>
      <input type="text" v-model="newTodoItem" @keyup.enter="addTodo"/>
      <button @click="addTodo">add</button>
    </div>
    <div>
      <input v-if="isEdit" type="text" v-model="editTodoItem" @keyup.enter="editTodo"/>
      <button v-if="isEdit" @click="editTodo">edit</button>
    </div>
    <TodoList
        :todo-array="todoArray"
        @fnEdit="fnEdit"
        @deleteTodo="deleteTodo"
        @clearTodo="clearTodo"
    ></TodoList>
  </div>
</template>

<script>
import TodoList from './TodoList.vue'

export default {
  data () {
    return {
      newTodoItem: '',
      editTodoItem: '',
      todoArray: [],
      isEdit: false,
      itemIndex: 0
    }
  },
  created () {
    if (localStorage.getItem('todolist')) {
      this.todoArray = JSON.parse(localStorage.getItem('todolist'))
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
        const itemInfo = { item: this.newTodoItem && this.newTodoItem.trim(), isCompleted: false }
        this.todoArray.push(itemInfo)
        this.newTodoItem = ''
        localStorage.setItem('todolist', JSON.stringify(this.todoArray))
      }
    },
    fnEdit (isEdit, index) {
      this.isEdit = isEdit
      this.editTodoItem = this.todoArray[index].item
      this.itemIndex = index
    },
    editTodo () {
      const itemArray = this.todoArray.map(todo => todo.item)
      if (itemArray.indexOf(this.editTodoItem) !== -1) {
        alert('이미 등록된 할일입니다.')
        return
      }
      this.todoArray = JSON.parse(localStorage.getItem('todolist'))
      this.todoArray[this.itemIndex].item = this.editTodoItem

      localStorage.setItem('todolist', JSON.stringify(this.todoArray))
      this.editTodoItem = ''
      this.isEdit = false
    },
    deleteTodo (index) {
      this.todoArray = JSON.parse(localStorage.getItem('todolist'))
      this.todoArray.splice(index, 1)

      localStorage.setItem('todolist', JSON.stringify(this.todoArray))
    },
    clearTodo () {
      localStorage.clear()
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
