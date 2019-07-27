<template>
  <div class="hello container">
    <div class="container col-md-6 col-sm-12">
      <div id="tasks">
        <div class="table-border p-5">
          <h1 class="text-left"> To do: </h1>
          <div class="table-border">
            <div class = "item-border container" v-for="id in tasks.length" :key="id" >
              <div class="row" :class="!tasks[id-1].completed ? 'complete': 'incomplete'">
                <input class="form-control col-md-8" 
                       v-model="tasks[id-1].body"
                       @click="incompleteTask(tasks[id-1])" />
                <div class="col-md-4 text-right">
                  <div class="">
                    <button id="toggleComplete" 
                          class="btn btn-success m-1 btn-width-38" 
                          @click="toggleComplete(tasks[id-1])">
                          <span v-if="!tasks[id-1].completed">✔</span>
                          <span v-if="tasks[id-1].completed"> &nbsp;</span>
                          </button>

                      <button id="deleteTask" 
                          class="btn glyphicon btn-danger btn-width-38"
                          @click="deleteTask(id-1)">
                            <span>X</span>
                      </button>  
                  </div>
                </div>
              </div>
            </div>
          </div>
          <form @submit="addTask" class="form-addtask">
            <div class="form-inline row">
              <div class="col-md-3">
                <label> Task </label>  
              </div>
              <div class="col-md-9 text-right">
              <input
                    type="text" 
                     class="form-control" placeholder="What do you need to do" 
                     v-model="newTask"
                     />
              </div>
            </div>
            <div class="form-group">
              <button type="submit" class="btn  btn-primary text-right" style="float: right;"> Save Item</button>
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
.hello {
  border-radius: .25rem;
  margin: 5rem 0rem;
  padding: 5em;
  margin-left: auto;
  margin-right:auto;

  .table-border{
    border: 1px solid #ced4da;
    border-radius: .25rem;
    margin-bottom: 0rem;
  }
  .item-border{
    border-bottom: 1px solid #ced4da;
    border-radius: .25rem;
    margin-bottom: 0rem;
  }

}

.from-addtask{
  margin-top: 5rem;
}

input, button {
  margin: 0.25rem 0rem;
}

.btn-width-38 {
  width: 38px;
}

input, pre, label{
  font-size: 20px !important;
}
.complete{
  #toggleComplete{
    color: #fff !important;
    border-color: #46b8da;
    content: "✔"
  }
  #deleteTask{
    color: #fff !important;
    background-color: #d9534f;
    border-color: #d43f3a;
   
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
    content : 'X'
  }
  #deleteTask{
    color: #fff !important;
    background-color: #d9534f;
    border-color: #d43f3a;
  }
  input{
      text-decoration: line-through;
      border: none;
      box-shadow: none;
      color: grey;
    
  }
}
.form-addtask {
  margin-top : 5rem;
  input {
    width: 100%;
  }
}
</style>
