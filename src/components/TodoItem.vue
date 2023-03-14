<template>
  <div class="todo-item">
    <div>
      <p :class="'content' + {' done' : item.done}" v-if="!isEditing">{{ item.content }}</p>
      <form v-else @submit.prevent="onSubmit">
        <input type="text" v-model="inputValue">
        <button type="submit">Update</button>
      </form>
    </div>
    <LittleBtn :content="item.done ? 'To do' : 'Done'" @click="$emit('clickTodo', item.id)" />
    <LittleBtn content="Update" @click="isEditing = true" />
    <LittleBtn content="Delete" @click="$emit('deleteTodo', item.id)" />
  </div>
</template>

<script>
import LittleBtn from './LittleBtn.vue'
export default {
  name: 'TodoItem',
  props: {
    item: Object
  },
  components: {
    LittleBtn
  },
  data () {
    return {
      isEditing: false,
      inputValue: ''
    }
  },
  created () {
    this.inputValue = this.item.content
  },
  methods: {
    onSubmit () {
      this.isEditing = false
      this.$emit('updateTodo', this.item.id, this.inputValue)
    }
  }
}
</script>

<style scoped lang="scss">
.todo-item {
  display: flex;
  gap: 10px;
  .content {
    .done {
      text-decoration: line-through;
    }
  }
}
</style>
