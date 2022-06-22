<template>
  <div class="home">
    <div class="todos" >
      <todo-item
        :todo="todo"
        v-for="todo in todos"
        :key="todo.id"
        @get-todo="$emit('get-todo', $event)"
      />
    </div>
  </div>
</template>

<script>
import TodoItem from './TodoItem.vue'

export default {
  name: 'HomeView',
  components: {
    TodoItem,
  },
  props: {
    todos: {
      type: Array
    }
  },
  methods: {
  }
}
</script>

<style scoped>
  .todos {
    margin-top: 32px;
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    gap: 30px;
  }
</style>
