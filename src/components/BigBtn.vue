<template>
  <button type="button" class="big-btn" @click="$emit('onClick')">
    {{ content }}
  </button>
</template>

<script>
export default {
  name: 'BigBtn',
  props: {
    content: String
  },
}
</script>

<style scoped lang="scss">
.big-btn {
  display: block;
  padding: 7px 15px;
  color: white;
  background-color: #41b883;
}
</style>
