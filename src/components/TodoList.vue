<template>
  <div>
    <ul class="todoListSection">
      <div>{{ msg }}</div>
      <li
          v-for="(todoItem, index) in todoArray"
          :key="index">
        <div class="listSection">
          <button @click="checkTodo(todoItem)" :class="{ isCheckedBtn: todoItem.isCompleted }">✔️</button>
            <span
                :class="{ isChecked: todoItem.isCompleted }"
                @click="checkTodo(todoItem)">
              {{ todoItem.item }}
            </span>
        </div>
        <div class="buttonSection">
          <button @click="editTodo(index)">✏️</button>
          <button @click="deleteTodo(index)">❌</button>
        </div>
      </li>
    </ul>
    <button class="clearBtn" @click="clearTodo">전체 삭제</button>
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
    todoArray: Array,
    msg: String
  },
  created () {
    console.log(this.todoArray)
  },
  methods: {
    checkTodo (todoItem) {
      todoItem.isCompleted = !todoItem.isCompleted
      this.$emit('checkTodo', todoItem)
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
div{
  .inputSection{
    input{
      width: 500px;
      height: 32px;
      font-size: 20px;
      border: 0;
      border-radius: 10px;
      outline: none;
      margin: 10px;
      padding-left: 5px;
      background-color: lightgray;
      font-family: 'SANGJUDajungdagam';
    }
    .inputBtn{
      border-radius: 10px;
      border: solid 1px;
      padding: 7px;
    }
  }
  button{
    border: none;
    background-color: white;
    cursor: pointer;
    transition: 0.5s;
    font-size: 1.1em;
    align-items: center;
    margin: 5px;
    &:hover { opacity: 50% }
  }
  .todoListSection{
    list-style: none;
    width: 500px;
    margin: 0 auto;
    padding: 30px;
    li{
      display: flex;
      padding: 5px;
      margin: 20px;
      border: solid 1px;
      border-radius: 10px;
      box-shadow: 3px 3px gray;
      font-size: 1.2em;
      .listSection{
        align-items: center;
        margin: 5px;
        span{
          cursor: pointer;
        }
        .isCheckedBtn{
          opacity: 60%;
        }
      }
      .buttonSection{
        margin-left: auto;
        padding: 5px;
        align-items: center;
      }
      .isChecked{
        text-decoration: line-through;
        opacity: 70%;
      }
    }
  }
  .clearBtn{
    border-radius: 10px;
    border: solid 1px;
    width: 100px;
    height: 50px;
    font-family: 'SANGJUDajungdagam';
  }
}
</style>
