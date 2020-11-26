<template>
  <div>
    <NavBar />
    <AddTodo @add-todo="addTodo"/>
    <div class="container">
      <Todos :todos="todos" @delete-todo="deleteTodo"/>
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
      todos: [
        {_id: uuidv4(), title: "Todo item 1", completed: false},
        {_id: uuidv4(), title: "Todo item 2", completed: false},
        {_id: uuidv4(), title: "Todo item 3", completed: false},
        {_id: uuidv4(), title: "Todo item 4", completed: false},
        {_id: uuidv4(), title: "Todo item 5", completed: false},
        {_id: uuidv4(), title: "Todo item 6", completed: false},
      ]
    }
  },
  methods: {
    addTodo(title){
      const newTodo = {
        _id: uuidv4(),
        title: title,
        completed: false
      };
      this.todos.push(newTodo);
    },
    deleteTodo(todoId){
      this.todos = this.todos.filter(todo => todo._id !== todoId);
    }
  }
}
</script>

<style>

</style>