<template>
  <div class="border-bottom bg-white">
      <form class="py-5 container" @submit.prevent="addTodo">
          <div class="form-row">
              <div class="input-group col-8">
                  <input v-model="title" type="text" class="form-control" :class="{'is-invalid': error}" placeholder="Add todo...">
                  <div class="input-group-append">
                      <button class="btn btn-info">Add</button>
                  </div>
                  <div class="invalid-feedback">Please enter Todo</div>
              </div>
              <select class="form-control col-4" v-model="select" @change="$emit('sort', select)">
                  <option value="">Show All</option>
                  <option value="false">Show uncompleted</option>
                  <option value="true">Show completed</option>
              </select>
          </div>
          
      </form>
  </div>
</template>

<script>
export default {
    data(){
        return {
            title: '',
            error: false,
            select: ''
        }
    },
    methods: {
        addTodo(){
            this.title = this.title.trim();
            if(this.title.length){
                this.$emit('add-todo', this.title);
                this.title = '';
                this.error = false;
            } else {
                this.error = true;
            }
        }
    }
}
</script>

<style>

</style>