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
      isEdit: false
    }
  },
  methods: {
    addTodo () {
      if (this.newTodoItem === '') {
        alert('할일을 입력하세요')
      } else {
        const itemArray = { item: this.newTodoItem && this.newTodoItem.trim(), isCompleted: false }
        this.todoArray.push(itemArray)
        this.newTodoItem = ''
        localStorage.setItem('todolist', JSON.stringify(this.todoArray))
        console.log(this.todoArray)
      }
    },
    editTodo () {
      console.log(this.editTodoItem)
      this.editTodoItem = ''
    },
    fnEdit (isEdit) {
      console.log(isEdit)
      this.isEdit = isEdit
      console.log(isEdit)
    }
  },
  components: {
    TodoList
  }
}
</script>

<style lang="scss">

</style>
