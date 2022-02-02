<template>
  <div class="inputSection">
    <div>
      <input type="text" v-model="newTodoItem" @keyup.enter="addTodo"/>
      <button class="inputBtn" @click="addTodo">add</button>
    </div>
    <div>
      <input v-if="isEdit" type="text" v-model="editTodoItem" @keyup.enter="editTodo"/>
      <button class="inputBtn" v-if="isEdit" @click="editTodo">edit</button>
    </div>
    <TodoList
        :todo-array="todoArray"
        :msg="msg"
        @fnEdit="fnEdit"
        @clearTodo="clearTodo"
        @deleteTodo="deleteTodo"
        @checkTodo="checkTodo"
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
      itemIndex: 0,
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
        const itemInfo = { item: this.newTodoItem && this.newTodoItem.trim(), isCompleted: false }
        this.todoArray.push(itemInfo)
        this.newTodoItem = ''
        localStorage.setItem('todolist', JSON.stringify(this.todoArray))
        this.msg = ''
      }
    },
    checkTodo (todoItem) {
      console.log(todoItem.isCompleted)
      localStorage.setItem('todolist', JSON.stringify(this.todoArray))
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
      console.log(this.todoArray.length === 0)
      if (this.todoArray.length === 0) {
        this.msg = '할일이 없어요.'
        console.log(this.msg)
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
