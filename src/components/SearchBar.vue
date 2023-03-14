<template>
  <input type="text" v-model="inputValue" placeholder="Search...">
</template>
  
<script>
export default {
  name: 'SearchBar',
  data () {
    return {
      inputValue: ''
    }
  },
  watch: {
    inputValue () {
      this.$emit('search', this.inputValue)
    }
  }
}
</script>

<style scoped lang="scss">

</style>
