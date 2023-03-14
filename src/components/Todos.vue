<template>
  <h1 class="title">To Do List</h1>
  <form @submit.prevent="createTodo(inputValue)">
    <input type="text" v-model="inputValue">
    <button type="submit">Add</button>
  </form>
  <div class="todo-list">
    <TodoItem v-for="todo in todos" :key="todo.id" :item="todo" @clickTodo="(id) => clickTodo(id)" @updateTodo="(id, content) => updateTodo(id, content)" @deleteTodo="(id) => deleteTodo(id)" />
  </div>
  <div class="btns">
    <BigBtn content="Clear List" @click="clearList" />
    <BigBtn content="Clear Complete" @click="completeClear" />
  </div>
</template>
  
<script>
import TodoItem from './TodoItem.vue'
import BigBtn from './BigBtn.vue'
export default {
  name: 'Todos',
  components: {
    TodoItem,
    BigBtn
  },
  data () {
    return {
      todos: [],
      tempId: 0,
      inputValue: ''
    }
  },
  computed: {
    todoId () {
      this.tempId++
      return this.tempId
    }
  },
  methods: {
    deleteTodo (todoId) {
      this.todo = this.todos.filter( (todo) => todo.id !== todoId)
    },
    clearList () {
      this.todo = this.todos.filter( (todo) => !todo.done)
    },
    completeClear () {
      this.todo = []
    },
    createTodo (content) {
      this.inputValue = ''
      this.todos.push({
        id: this.todoId,
        content,
        done: false
      })
    },
    updateTodo (id, content) {

    },
    clickTodo (id) {

    }
  }
}
</script>

<style scoped lang="scss">
.title {
  color: white;
  background-color: #41b883;
  padding: 10px 50px;
}
.btns {
  display: flex;
  gap: 20px;
  justify-content: center;
}
</style>
