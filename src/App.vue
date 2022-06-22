<template>
  <div id="app">
    <div class="container">
      <nav>
        <router-link to="/">Home</router-link> |
        <router-link to="/create">Create</router-link>
      </nav>
      <router-view :todos="todos" @get-todo="getActiveTodo($event)" :activeTodo="activeTodo" @save-todo="saveTodo($event)" @delete-todo="deleteTodo($event)" />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeTodo: {},
      todos: [
        { id: 1, name: 'Задание на сегодня', todoList: [{ id: 1, name: 'Сделать это 1', completed: true }, { id: 2, name: 'Сделать это 2', completed: false }, { id: 3, name: 'Сделать это 3', completed: false }, { id: 4, name: 'Сделать это 1', completed: true }, { id: 5, name: 'Сделать это 1', completed: true }, { id: 6, name: 'Сделать это 1', completed: true }]},
        { id: 2, name: 'Задание на завтра', todoList: [{ id: 1, name: 'Сделать это 1', completed: false }, { id: 2, name: 'Сделать это 2', completed: false }, { id: 3, name: 'Сделать это 3', completed: false } ]},
        { id: 3, name: 'Задание на вторник', todoList: [{ id: 1, name: 'Сделать это 1', completed: false }, { id: 2, name: 'Сделать это 2', completed: false }, { id: 3, name: 'Сделать это 3', completed: false } ]}
      ]
    }
  },
  methods: {
    getActiveTodo(event) {
      this.activeTodo = event
    },
    saveTodo(newTodo) {
      let id = newTodo.id
      this.todos.forEach((el) => {
        if (el.id == id) {
          el = newTodo
        }
      })
    },
    deleteTodo(Todo) {
      let id = Todo.id
      this.todos = this.todos.filter(el => el.id != id)
      console.log(this.todos);
    }
  }
}
</script>

<style>
@import '@/assets/css/style.css';

</style>