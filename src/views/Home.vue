<template>
  <div id="app">
    <!-- <Header /> -->
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" 
      v-on:del-todo="deleteTodo"
    />
  </div>
</template>

<script>

// import Header from '../components/layout/Header';
import Todos from '../components/Todos';
import AddTodo from '../components/AddTodo';
import axios from 'axios';

export default {
  name: 'Home',
  components: {
    // Header,
    Todos,
    AddTodo
  },
  data() {
    return {
    //   todos: [
    //     {
    //       id: 1,
    //       title: "List all you want",
    //       completed: true
    //     },
    //     {
    //       id: 2,
    //       title: "Organize it or group it together",
    //       completed: false
    //     },
    //     {
    //       id: 3,
    //       title: "Think of a plan to reach it",
    //       completed: false
    //     },
    //     {
    //       id: 4,
    //       title: "Start executing the plan!",
    //       completed: false
    //     }
    //   ]
    // }

    // I commmented the above static data, because now we will be calling an api to populate our data
    todos: [
        
      ]
    }
  },
  methods: {
    deleteTodo(id) {
      // this.todos = this.todos.filter(todo => todo.id !== id);
      axios.delete(`https://jsonplaceholder.typicode.com/todos${id}`)
        .then(this.todos = this.todos.filter(todo => todo.id !== id))
        .catch(err=> console.log(err));
    },
    addTodo(newTodo) {
      // console.log(123);
      const { title, completed } = newTodo;

      axios.post('https://jsonplaceholder.typicode.com/todos',{
        title,
        completed
      })
        .then(res =>  this.todos = [...this.todos, res.data])
        .catch(err=> console.log(err));
      // this.todos = [...this.todos, newTodo];
    }
  },
  // default on js which runs on start
  created(){

    // you need axios for this | to perform http request
    // npm i axios
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=8')
      .then(res => this.todos = res.data)
      .catch(err=> console.log(err));
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

  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }

  .btn:hover {
    background: #667
  }
</style>
