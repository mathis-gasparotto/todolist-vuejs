<template>
  <h1 class="title">To Do List</h1>
  <form @submit.prevent="createTodo(inputValue)">
    <input type="text" v-model="inputValue">
    <button type="submit">Add</button>
  </form>
  <div class="todo-list">
    <TodoItem v-for="todo in todos" :key="todo.id" :item="todo" @toggleTodo="(id) => toggleTodo(id)" @updateTodo="(id, content) => updateTodo(id, content)" @deleteTodo="(id) => deleteTodo(id)" />
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
  methods: {
    deleteTodo (todoId) {
      this.todos = this.todos.filter( (todo) => todo.id !== todoId)
    },
    clearList () {
      this.todos = this.todos.filter( (todo) => !todo.done)
    },
    completeClear () {
      this.todos = []
    },
    createTodo (content) {
      if(!content) {
        return
      }
      this.inputValue = ''
      this.todos.push({
        id: this.todoId(),
        content,
        done: false
      })
    },
    updateTodo (id, content) {
      this.todos.forEach((e) => {
        if (e.id === id) {
          e.content = content
        }
      })
    },
    toggleTodo (id) {
      this.todos.forEach((e) => {
        if (e.id === id) {
          e.done = !e.done
        }
      })
    },
    todoId () {
      this.tempId = this.tempId + 1
      return this.tempId
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
