<template>
  <div>
    <ul>
      <span>{{ message }}</span>
      <li
          v-for="(todoItem, index) in todoArray"
          :key="index">
        <div>
          <button @click="checkTodo(todoItem)">✔️</button>
          <span>{{ todoItem.item }}</span>
          <button @click="editTodo(index)">수정</button>
          <button @click="deleteTodo(index)">삭제</button>
        </div>
      </li>
    </ul>
    <button @click="clearTodo">전체 삭제</button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      isEdit: false,
      message: ''
    }
  },
  props: {
    todoArray: Array
  },
  created () {
    console.log(this.todoArray)
  },
  methods: {
    checkTodo (todoItem) {
      console.log(todoItem.isCompleted)
      if (todoItem.isCompleted) {
        todoItem.isCompleted = false
      } else {
        todoItem.isCompleted = true
      }
      console.log(this.todoArray)
      // todoItem.isCompleted = todoItem.isCompleted === true ? false : true
    },
    editTodo (index) {
      if (this.isEdit) {
        this.isEdit = false
      } else {
        this.isEdit = true
      }
      this.$emit('fnEdit', this.isEdit, index)
    },
    deleteTodo (index) {
      this.$emit('deleteTodo', index)
    },
    clearTodo () {
      this.$emit('clearTodo')
    }
  }
}
</script>

<style lang="scss">

</style>
