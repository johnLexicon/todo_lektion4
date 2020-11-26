<template>
  <div v-if="todos.length">
      <div v-for="todo in todos" :key="todo._id">
          <Todo :todo="todo" @delete-todo="$emit('delete-todo', todo._id)" />
      </div>
  </div>
  <div v-else>
      <p>No todos left</p>
  </div>
</template>

<script>
import Todo from './Todo';

export default {
    props: ['todos'],
    components: {
        Todo
    }
}
</script>

<style>

</style>