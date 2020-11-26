<template>
  <div>
    <div class="d-flex justify-content-between align-items border p-2 m-1 bg-white">
        <p class="m-0" :class="{done: todo.completed}" @click="toggleComplete">{{ todo.title }}</p>
        <button class="btn btn-danger px-3" @click="$emit('delete-todo', todo._id)">X</button>
    </div>    
  </div>
</template>

<script>
export default {
    props: ['todo'],
    methods: {
        toggleComplete(){
            this.$emit('toggle-complete', this.todo._id);
        }
    }
}
</script>

<style scoped>
    .done{
        text-decoration: line-through;
        color: #bbb;
    }
    p{
        cursor: pointer;
    }
</style>