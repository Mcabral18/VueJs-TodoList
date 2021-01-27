<template>
	<div id="app">
		<h1>TodoList</h1>
		<task-progress :progress="progress"/>
		<new-task @taskAdded="addTask"/>
		<task-grid :tasks="tasks" @taskDeleted="deleteTask" @taskStateChange="toggleTaskState"/>
	</div>
</template>

<script>
import TaskGrid from "@/components/TaskGrid.vue";
import NewTask from "./components/NewTask.vue";
import TaskProgress from './components/TaskProgress.vue';
export default {
  components: { TaskGrid, NewTask, TaskProgress },
  data() {
    return {
      tasks: [
        // now we can add task we dont need this model array
        // {name: 'Lavar a louça', pending: false},
        // {name: 'Comprar Cafe', pending: true},
      ]
    };
  },
  methods: {
    addTask(task) {
      // uncomment the code bellow to set a verification if the todo already exist we cant add one with the same name
      // const sameName = t => t.name === task.name
      // const reallyNew = this.tasks.filter(sameName).length == 0
      // if(reallyNew){
      this.tasks.push({
        name: task.name,
        pending: task.pending || true
      });
      // }
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    toggleTaskState(index) {
      this.tasks[index].pending = !this.tasks[index].pending
    }
  },
  computed:{
	  progress(){
		 const total = this.tasks.length
		 const done = this.tasks.filter(t=> !t.pending).length
		 return Math.round(done / total * 100) || 0 
	  }
  },
  watch:{
    // monitora o array sempre que ele mudar chama esta funçao
    //pego as tasks converto para string e estou a armazenar 
    // tasks(){
    //   localStorage.setItem("tasks", JSON.stringify(this.tasks));
    // }
    // using watch deep - tell watch method to look deeper inside the array/object
    tasks: {
      // This will let Vue know to look inside the array
      deep: true,
      // We have to move our method to a handler field
      handler() {
        localStorage.setItem("tasks", JSON.stringify(this.tasks));
      }
    }
  },
  created(){
    // a variable json vai conter os tasks em formato string
    const json = localStorage.getItem("tasks"); 
    // console.log(json)
    // this.tasks contem a valor de json
    this.tasks = JSON.parse(json)
  }
};
</script>

<style>
body {
  font-family: "Lato", sans-serif;
  background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
  color: #fff;
}

#app {
  display: flex;
  flex: 1;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

#app h1 {
  margin-bottom: 5px;
  font-weight: 300;
  font-size: 3rem;
}
</style>
