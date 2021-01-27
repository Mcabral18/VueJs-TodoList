<template>
  <div class="new-task">
      <input v-model="name" @keydown.prevent.enter="addTodo" type="text"
      class="form-element" placeholder="New Todo!"
      >
      <button class="form-element" @click.prevent="addTodo">+</button>
  </div>
</template>

<script>
export default {
    data(){
        return{
            name: ""
        }
    },
    methods: {
        addTodo(){
           this.$emit('taskAdded', {name: this.name})
           this.name = ""
        }
    }
}
</script>

<style>
.form-element{
    outline: none;
    font-size: 1.3em;
    border: 1px solid #fff;
    padding: 5px 10px 8px;
    color: #fff
}

input.form-element{
    width: 450px;
    background: #fff2;
    border-top-left-radius: 8px;
    border-bottom-left-radius: 8px;
}

button.form-element{
    border-left: none;
    background-color: #2196F3;
    border-top-right-radius: 8px;
    border-bottom-right-radius: 8px;
}

</style>