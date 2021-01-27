<template>
  <div @click="$emit('taskStateChange', task)" class="task" :class="stateClass">
    <p>{{ task.name }}</p>
    <span @click.stop="$emit('taskDeleted', task)" class="close">X</span>
  </div>
</template>

<script>
export default {
  props: {
    task: {
      type: Object,
      requiered: true,
    },
  },
  computed: {
    // Swith between done and pending and change color of the task to green or red
    stateClass() {
      return {
        pending: this.task.pending,
        done: !this.task.pending,
      };
    },
  },
};
</script>

<style>
.btn {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0px 10px;
  background-color: transparent;
  color: #fff;
  border: 1px solid grey;
}

.task {
  position: relative;
  box-sizing: border-box;
  width: 200px;
  height: 50px;
  padding: 10px;
  font-size: 1em;
  cursor: pointer;
  user-select: none;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 10px 0;
}

.pending {
  border-left: 10px solid red;
  background-color: rgb(117, 45, 45);
}

.done {
  border-left: 10px solid green;
  background-color: rgb(92, 221, 92);
  text-decoration: line-through;
}
.pending .close {
  background-color: red;
}
.done .close {
  background-color: green;
}
.close {
  position: absolute;
  top: 5px;
  right: 5px;
  font-size: 0.9em;
  font-weight: 600;
  height: 20px;
  width: 20px;
  border-radius: 10px;
  display: flex;
  justify-content: center;
}
</style>