<template>
  <div>
    <ul>
      <span>message</span>
      <li
          v-for="(todoItem, index) in todoArray"
          :key="index">
        <div>
          <span>{{ todoItem.item }}</span>
          <button @click="editTodo">수정</button>
          <button>삭제</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data () {
    return {
      isEdit: false
    }
  },
  props: {
    todoArray: Array
  },
  created () {
    console.log(this.todoArray)
  },
  methods: {
    editTodo () {
      if (this.isEdit) {
        this.isEdit = false
      } else {
        this.isEdit = true
      }
      this.$emit('fnEdit', this.isEdit)
    }
  }
}
</script>

<style lang="scss">

</style>
