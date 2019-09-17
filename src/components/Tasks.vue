<template>
  <b-row class="justify-content-center">
    <b-col col cols="8">
      <h1>Your tasks</h1>
      <div class="tasks">
        <div>
          <b-form-input
            v-model="newTask"
            placeholder="Your new task"
            @keyup.enter="addTask"
          >
          </b-form-input>
          <p>
            Type in your new task above and press enter. Your task will be added
            to your list.
          </p>
        </div>
        <div class="options">
          <b-button @click="filter = 'all'" :variant="filter === 'all' ? 'primary' : 'secondary'"  size="sm">
            All
          </b-button>
          <b-button @click="filter = 'completed'" :variant="filter === 'completed' ? 'primary' : 'secondary'" size="sm">
            Completed
          </b-button>
          <b-button @click="filter = 'uncompleted'" :variant="filter === 'uncompleted' ? 'primary' : 'secondary'" size="sm">
            Uncompleted
          </b-button>
        </div>
        <Task
          v-for="task in visibleTasks"
          :key="task.id"
          :task="task"
          @completeTask="complete"
          @deleteTask="deleteTask(task.id)"
        >
        </Task>
        <div class="text-right">
          &nbsp;
          <b-button
            v-if="!isAllCompleted"
            @click="completeAllTask"
            variant="info"
            size="sm"
          >
            Check All
          </b-button>
          <b-button
            v-if="isAllCompleted"
            @click="uncompleteAllTask"
            variant="info"
            size="sm"
          >
            Uncheck All
          </b-button>
        </div>
      </div>
    </b-col>
  </b-row>
</template>

<script>
import Task from "../components/Task.vue";

export default {
  name: "Tasks",
  data() {
    return {
      newTask: "",
      tasks: [],
      filter: 'all',
    };
  },
  mounted(){
    this.tasks = localStorage.getItem('tasks') !== null ? JSON.parse(localStorage.getItem('tasks')) : [];
  },
  watch: {
    tasks: function(){
      this.save();
    }
  },
  computed: {
    isAllCompleted: function() {
      let result = true;
      this.tasks.forEach(task =>
        task.complete === false ? (result = false) : null
      );
      return result;
    },
    visibleTasks: function () {
      if(this.filter === 'all'){
        return this.tasks;
      }
      if (this.filter === 'completed') {
        return this.tasks.filter(task => task.complete);
      }
      if (this.filter === 'uncompleted') {
        return this.tasks.filter(task => !task.complete);
      }
    }
  },
  methods: {
    newId: function() {
      let id =
        this.tasks.length !== 0
          ? Math.max(...this.tasks.map(task => task.id))
          : 0;
      return id;
    },
    addTask: function() {
      if (this.newTask.length !== 0)
        this.tasks.push({
          id: this.newId() + 1,
          content: this.newTask,
          complete: false
        });

      this.newTask = "";
      this.save();
    },
    editTask: function(obj){
      this.tasks = this.tasks.map(task => {
        if(task.id !== obj.id) return task;
        else task.content = obj.newVal;
        return task;
      });
      this.save();
    },
    save: function(){
      localStorage.setItem('tasks',JSON.stringify(this.tasks));
    },
    complete: function(obj){
      this.task = this.tasks.map(task => {if(task.id !== obj.id) return task; else task.complete = obj.status; return task;});
      this.save();
    },
    completeAllTask: function() {
      this.tasks.forEach(task => (task.complete = true));
      this.save();
    },
    uncompleteAllTask: function() {
      this.tasks.forEach(task => (task.complete = false));
      this.save();
    },
    deleteTask: function(id) {
      this.tasks = this.tasks.filter(task => task.id !== id);
      this.save();
    }
  },
  components: {
    Task
  }
};
</script>

<style lang="scss">
.tasks {
  margin-top: 40px;

  p {
    margin-left: 0.3em;
    line-height: 2em;
  }

  .options {
    margin: 0 0 30px 0;
  }

  .task {
    font-size: 1.4em;
    line-height: 1.3em;
    height: 50px;
  }

  button {
    margin: 0 5px;
    line-height: 1em;
  }
}
</style>
