<template>
  <div v-if="todos.length">
      <div v-for="todo in todos" :key="todo._id">
          <Todo v-if="sortValue === ''" :todo="todo" @delete-todo="$emit('delete-todo', todo._id)" />
          <Todo v-if="sortValue === todo.completed" :todo="todo" @delete-todo="$emit('delete-todo', todo._id)" />
      </div>
  </div>
  <div v-else>
      <p>No todos left</p>
  </div>
</template>

<script>
import Todo from './Todo';

export default {
    props: ['todos', 'sortValue'],
    components: {
        Todo
    }
}
</script>

<style>

</style>