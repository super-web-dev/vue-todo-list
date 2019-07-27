<template>
  <div class="hello card">
    <h1> To do: </h1>
    <div class="container">
      <div id="tasks">
        <div class="col-md-6">
          
          <div v-for="id in tasks.length" :key="id">

            <p class="form-inline" :class="!tasks[id-1].completed ? 'complete': 'incomplete'">
              <input class="form-control" 
                     v-model="tasks[id-1].body"
                     @click="incompleteTask(tasks[id-1])">

              <button id="toggleComplete" 
                      class="btn glyphicon" 
                      @click="toggleComplete(tasks[id-1])"></button>

              <button id="deleteTask" 
                      class="btn glyphicon"
                      @click="deleteTask(id-1)"></button>
            </p>
          </div>
          <form @submit="addTask">
            <div class="form-inline">
              <input type="text" 
                     class="form-control" placeholder="I need to..." 
                     v-model="newTask" 
                     />
              <button type="submit" class="btn  btn-primary" >Add</button>
            </div>
          </form>
        </div>

      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() { return {
      tasks: [{
        "body": "Learn Vue.js",
        "completed": false
      }],
      newTask: ''
    }
  },
  computed: {
    completedTasks: function(){
      return this.tasks.filter(function(task){
        return task.completed;
      });
    },
    remainingTasks: function(){
      return this.tasks.filter(function(task){
        return ! task.completed;
      });
    },
  },
  methods: {
    addTask: function(e) {
      e.preventDefault();
      if (this.newTask == '') return;
      this.tasks.push({
        body: this.newTask,
        completed: false
      });
      this.newTask = ''
    },
    deleteTask: function(task_id){
      this.$delete(this.tasks, task_id);
    },
    toggleComplete: function(task){
      task.completed = ! task.completed;
    },
    incompleteTask: function(task){
      task.completed = false;
    },
  }
}
</script>

<style lang="scss" scoped>
input, pre {
  font-size: 20px !important;
}
.complete{
  #toggleComplete{
    color: #fff !important;
    background-color: #5bc0de;
    border-color: #46b8da;
    &:before{
      content: "\e013"
    }
  }
  #deleteTask{
    color: #fff !important;
    background-color: #d9534f;
    border-color: #d43f3a;
    &:before{
      content: "\e014"
    }
  }
  input{
      border: none;
      box-shadow: none;   
    &:focus{
      box-shadow: none;   
    }
  }
  
}

.incomplete{
  #toggleComplete{
    color: #fff !important;
    &:before{
      content: "\2212"
    }
  }
  #deleteTask{
    color: #fff !important;
    background-color: #d9534f;
    border-color: #d43f3a;
    &:before{
      content: "\e014"
    }
  }
  input{
      text-decoration: line-through;
      border: none;
      box-shadow: none;
      color: grey;
    
  }
}
</style>
