<template>
  <ul>
    <li><input type="text" v-model="addForm.title" /></li>
    <li><input type="date" v-model="addForm.deadlineAt"></li>
    <li><button v-on:click="addTodo">追加</button></li>
  </ul>
</template>

<script>
export default {
  name: 'TodoAddForm',
  props: {
    addForm: Object
  },
  methods: {
    addTodo () {
      this.$emit('addTodo')
    }
  }
}
</script>

<style scoped>

</style>
