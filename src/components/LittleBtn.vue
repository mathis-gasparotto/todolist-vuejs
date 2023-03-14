<template>
  <button type="button" class="little-btn" @click="$emit('onClick')">
    {{ content }}
  </button>
</template>

<script>
export default {
  name: 'LittleBtn',
  props: {
    content: String
  },
}
</script>

<style scoped lang="scss">
.little-btn {
  display: block;
  padding: 2px 5px;
  color: white;
  background-color: #41b883;
}
</style>
