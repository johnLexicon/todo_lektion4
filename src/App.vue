<template>
  <div>
    <NavBar />
    <AddTodo @add-todo="addTodo" @sort="sortTodos" />
    <div class="container">
      <Todos :todos="todos" :sortValue="sort" @delete-todo="deleteTodo" @toggle-complete="updateTodo"/>
    </div>
  </div>
</template>

<script>
import { v4 as uuidv4 } from 'uuid';
import NavBar from './components/NavBar';
import Todos from './components/todos/Todos';
import AddTodo from './components/todos/AddTodo';
export default {
  name: 'App',
  components: {
    NavBar,
    Todos,
    AddTodo
  },
  data(){
    return {
      todos: [],
      sort: ''
    }
  },
  methods: {
    addTodo(title){
      const newTodo = {
          _id: uuidv4(),
          title: title,
          completed: false
      };

      fetch('http://localhost:8080/api/todos', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(newTodo)
      })
      .then(() => this.fetchTodos())
      .catch(err => console.log(err));
    },
    deleteTodo(todoId){
      this.todos = this.todos.filter(todo => todo._id !== todoId);
      fetch(`http://localhost:8080/api/todos/${todoId}`, {
        method: 'delete'
      })
      .then(() => this.fetchTodos())
      .catch(err => console.log(err));
    },
    updateTodo(todoId){
      let {completed } = this.todos.find(todo => todo._id === todoId);
      completed = !completed;

      fetch(`http://localhost:8080/api/todos/${todoId}`, {
        method: 'PATCH',
        body: JSON.stringify({ completed }),
        headers: {
          'Content-type': 'application/json'
        }
      })
      .then(response => response.json())
      .then(data => { console.log(data); this.fetchTodos(); })
      .catch(err => console.log(err))
    },
    sortTodos(value){
      switch(value){
        case 'false':
          this.sort = false;
          break;
        case 'true':
          this.sort = true;
          break;
        default:
          this.sort = ''
      }
    },
    fetchTodos(){
      fetch('http://localhost:8080/api/todos')
        .then(response => response.json())
        .then(data => this.todos = data)
        .catch(err => console.log(err));
    }
  },
  created(){
    this.fetchTodos();
  }
}
</script>

<style>

</style>