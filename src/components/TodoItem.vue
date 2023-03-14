<template>
  <div class="todo-item">
    <div>
      <p :class="'content' + (item.done ? ' done' : '')" v-if="!isEditing">{{ item.content }}</p>
      <form v-else @submit.prevent="onSubmit">
        <input type="text" v-model="item.content">
        <button type="submit">Update</button>
      </form>
    </div>
    <LittleBtn :content="item.done ? 'To do' : 'Done'" @onClick="$emit('toggleTodo', item.id)" />
    <LittleBtn content="Update" @onClick="isEditing = true" />
    <LittleBtn content="Delete" @onClick="$emit('deleteTodo', item.id)" />
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
      isEditing: false
    }
  },
  methods: {
    onSubmit () {
      this.isEditing = false
      this.$emit('updateTodo', this.item.id, this.item.content)
    }
  }
  
}
</script>

<style scoped lang="scss">
.todo-item {
  display: flex;
  gap: 10px;
  .content {
    margin: 0;
    &.done {
      text-decoration: line-through;
    }
  }
}
</style>
