<template>
  <div class="tasks">
    <template v-if="tasks.length > 0">
      <task v-for="(task, index) in tasks" :key="index" :task="task" @taskDeleted="$emit('taskDeleted', index)" @taskStateChange="$emit('taskStateChange', index)">
          <!-- $event invez do index serve para passar o parametro/evento que veio do filho -->
      </task>
    </template>
    <p v-else>All Done!</p>
  </div>
</template>

<script>
import Task from "./Task.vue";
export default {
  components: { Task },
  props: {
    //props validation
    tasks: { type: Array, required: true },
  },
};
</script>

<style>
</style>
