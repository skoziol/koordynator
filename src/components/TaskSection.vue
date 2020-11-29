<template>
    <div class="tasks-section">
      <h3>Zadania</h3>
      <span v-if="taskList.length > 0">{{completedTasks/taskList.length * 100}}%</span>  <progress :max="taskList.length" :value="completedTasks" v-if="taskList.length > 0"></progress>
      <div class="task" v-for="task in taskList" :key="task">
        <input ref="taskCheckbox" type="checkbox" v-model="task.status" @change="taskCompeted(task.status)">
        <span :class="{'line-through': task.status}">{{task.name}}</span>
        <button>przypisz do experta</button>
      </div>
      <div class="addTask">
        <input type="text" v-model="newTaskName">
        <button @click="addTask()">Add</button>
      </div>
  </div>
</template>

<script>
export default {
  name: 'tasks',
   data () {
    return {
      completedTasks: 0,
      newTaskName:'',
      taskList: []
    }
  },
  methods: {
    addTask() {
      if(this.newTaskName.length === 0) return
      this.taskList.push({
          name: this.newTaskName,
          status: false
        })
      this.newTaskName = ''
    },
    taskCompeted(){
      this.completedTasks = 0
      this.taskList.map(task => {
        if(task.status) this.completedTasks ++
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.tasks-section{
  flex-grow:1;
  .task{
    display:flex;
    align-items: center;
    justify-content: start;
    font-size: 15px;

    button{
      align-self: flex-end;
    }

    .line-through{
      text-decoration: line-through;
    }
  }

  .addTask{
  display:flex;
  } 
}
</style>