<template>
  <div>
    <todo-search-form v-bind:searchForm="searchForm" />
    <todo-add-form :add-form="this.addForm" v-on:addTodo="addTodo()" />
    <ul v-for="item in filteredItems" v-bind:key="item.id">
      <li>
        <ul>
          <li><input type="checkbox" v-model="item.checked"/>{{ item.title }} 期限: {{ item.deadlineAt}} 登録日: {{ item.createdAt }}<button v-on:click="deleteItem(item.id)">削除</button></li>
        </ul>
      </li>
    </ul>
  </div>
</template>

<script>
import TodoSearchForm from './components/TodoSearchForm'
import TodoAddForm from './components/TodoAddForm'
export default {
  name: 'App',
  data () {
    return {
      nextItemsId: 2,
      items: [
        {id: 1, checked: true, title: 'テスト', deadlineAt: '2019-04-10', createdAt: new Date()}
      ],
      searchForm: {
        text: '',
        filterChecked: false,
        unFilterChecked: false,
        sortColumn: ''
      },
      addForm: {
        title: '',
        deadlineAt: ''
      }
    }
  },
  components: {TodoSearchForm, TodoAddForm},
  computed: {
    filteredItems () {
      const filterResult = this.filterItems()
      const sortedResult = this.sortedItems(filterResult)
      return sortedResult
    }
  },
  methods: {
    addTodo () {
      const newTodo = this.buildTodo()
      this.items.push(newTodo)
      this.resetForm()
      this.nextItemsId += 1
    },
    resetForm () {
      this.addForm = {deadlineAt: '', title: ''}
    },
    buildTodo () {
      return {id: this.nextItemsId, checked: false, title: this.addForm.title, deadlineAt: this.addForm.deadlineAt, createdAt: new Date()}
    },
    filterItems () {
      const {filterChecked, unFilterChecked, text} = this.searchForm
      const result = this.items.filter(item => item.title.indexOf(text) > -1)
      if (filterChecked && unFilterChecked) {
        return result
      }
      if (filterChecked) {
        return result.filter(item => item.checked)
      }
      if (unFilterChecked) {
        return result.filter(item => !item.checked)
      }
      return result
    },
    sortedItems (items) {
      const {sortColumn} = this.searchForm
      console.log(sortColumn)
      if (!sortColumn.length) {
        return items
      }
      if (sortColumn === 'createdAtDesc') {
        return items.sort((a, b) => {
          if (a.createdAt > b.createdAt) {
            return -1
          } else if (a.createdAt < b.createdAt) {
            return 1
          }
        })
      } else if (sortColumn === 'deadlineAtAsc') {
        return items.sort((a, b) => {
          if (a.deadlineAt > b.deadlineAt) {
            return 1
          } else if (a.deadlineAt < b.deadlineAt) {
            return -1
          }
        })
      }
    },
    deleteItem (id) {
      this.items = this.items.filter(item => item.id !== id)
    }
  }
}
</script>

<style>
  ul {
    list-style: none;
  }
</style>
