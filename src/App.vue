<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Todos from './components/Todos'
import Header from './components/layout/Header'
import AddTodo from './components/AddTodo'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    Todos,
    Header,
    AddTodo
  },
  data() {
    return {
      todos: []
    }
  },
  methods: {
    deleteTodo(id) {
      console.log(id)
      this.todos = this.todos.filter((todo) => todo.id != id)
    },
    addTodo(newTodo) {
      this.todos = [...this.todos, newTodo]
    }
  },
  created() {
    console.log('hello')
    axios
      .get('https://jsonplaceholder.typicode.com/todos?_limit=10')
      .then((res) => (this.todos = res.data))
      .catch((error) => console.log(error))
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
</style>
