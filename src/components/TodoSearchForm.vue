<template>
  <ul>
    <li><input type="text" v-model="searchForm.text"></li>
    <li><input type="checkbox" v-model="searchForm.filterChecked">完了</li>
    <li><input type="checkbox" v-model="searchForm.unFilterChecked">未完了</li>
    <li>
      <select v-model="searchForm.sortColumn">
        <option value="" v-bind:key="1">選択してください</option>
        <option value="createdAtDesc" v-bind:key="2">登録順(降順)</option>
        <option value="deadlineAtAsc" v-bind:key="3">期限順(昇順)</option>
      </select>
    </li>
  </ul>
</template>

<script>
export default {
  name: 'TodoSearchForm',
  props: {
    searchForm: Object
  }
}
</script>

<style scoped>

</style>
