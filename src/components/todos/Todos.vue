<template>
  <div v-if="todos.length">
      <transition-group name="todos">
          <div v-for="todo in todos" :key="todo._id">
              <Todo v-if="sortValue === ''" :todo="todo" @delete-todo="$emit('delete-todo', todo._id)" @toggle-complete="$emit('toggle-complete', todo._id)" />
              <Todo v-else-if="sortValue === todo.completed" :todo="todo" @delete-todo="$emit('delete-todo', todo._id)" @toggle-complete="$emit('toggle-complete', todo._id)" />
          </div>
      </transition-group>
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

<style scoped>
    .todos-enter-active, .todos-leave-active {
        transition: all 0.5s ease;
    }
    .todos-enter {
        opacity: 0;
        transform: translateX(-30px);
    }
    .todos-leave-to {
        opacity: 0;
        transform: translateY(100px);
    }
</style>