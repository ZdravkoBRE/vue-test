<template>
  <div id="app">
    {{wMobile}}
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-bind:wMobile="wMobile" v-on:del-todo="deleteTodo"></Todos>
  </div>
</template>

<script>
import '../../public/scss/main.scss';

import Todos from '../components/Todos';
import AddTodo from '../components/AddTodo';
import axios from 'axios';

export default {
  name: 'home',
  components: {
    Todos,
    AddTodo
  },
  data() {
    return {
      todos: [],
      wMobile: false
    }
  },
  methods: {
    deleteTodo(id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(res => {
        this.todos = this.todos.filter(todo => todo.id !== id);
      })
      .catch(err => console.log(err));
    },

    addTodo(newTodo){
      const { title, completed } = newTodo;
      if (newTodo.title){
        axios.post('https://jsonplaceholder.typicode.com/todos', {
          title,
          completed
        })
        .then(res => {
          this.todos = [...this.todos, res.data];
        })
        .catch(err => console.log(err));
      }
      else
        alert("Plese insert title");
    },

    handleResize() {
      if ( window.innerWidth < 768){
        // block.className = block.className.replace(/\bbla\b/g, "");
        this.wMobile = true;
      } else {
        this.wMobile = false;
      }

    }

  }, 
  created() {

    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5&_page=10')
    .then(res => { 
      this.todos = res.data;
    })
    .catch(err => console.log(err));

    window.addEventListener('resize', this.handleResize);
    this.handleResize();
  },
  destroyed() {
    window.removeEventListener('resize', this.handleResize);
  },
}
</script>

<style>
*{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body{
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
</style>
