<template>
  <h1 class="title">To Do List</h1>
  <input type="text" v-model="strToSeach" placeholder="Search...">
  <form @submit.prevent="createTodo(inputValue)">
    <input type="text" v-model="inputValue">
    <button type="submit">Add</button>
  </form>
  <h2>To Do</h2>
  <div class="todo-list">
    <TodoItem v-for="todo in todosTodo" :key="todo.id" :item="todo" @toggleTodo="(id) => toggleTodo(id)" @updateTodo="(id, content) => updateTodo(id, content)" @deleteTodo="(id) => deleteTodo(id)" />
    </div>
  <h2>Done</h2>
  <div class="done-list">
    <TodoItem v-for="todo in todosDone" :key="todo.id" :item="todo" @toggleTodo="(id) => toggleTodo(id)" @updateTodo="(id, content) => updateTodo(id, content)" @deleteTodo="(id) => deleteTodo(id)" />
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
      inputValue: '',
      strToSeach: ''
    }
  },
  computed: {
    searchedTodo () {
      return this.strToSeach.length ? this.todos.filter((e) => e.content.search(this.strToSeach) !== -1) : this.todos
    },
    todosTodo () {
      return this.searchedTodo.filter((e) => !e.done)
    },
    todosDone () {
      return this.searchedTodo.filter((e) => e.done)
    }
  },
  methods: {
    deleteTodo (todoId) {
      this.todos = this.todos.filter((e) => e.id !== todoId)
    },
    clearList () {
      this.todos = this.todos.filter( (todo) => !todo.done)
    },
    completeClear () {
      this.todos = []
    },
    createTodo (content) {
      content = content.trim()
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
      this.todos.find((e) => e.id === id).content = content
    },
    toggleTodo (id) {
      this.todos.find((e) => e.id === id).done = !this.todos.find((e) => e.id === id).done
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
  margin-top: 40px;
}
</style>
