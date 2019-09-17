<template>
  <b-row class="justify-content-center">
    <b-col col cols="8">
      <h1>Your tasks</h1>
      <div class="tasks">
        <div class="mb-5">
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
        <Task
          v-for="task in tasks"
          :key="task.id"
          :task="task"
          @deleteTask="deleteTask(task.id)"
        >
        </Task>
        <div class="text-right">
          &nbsp;
          <b-button @click="switchAllTask" :variant="color" size="sm">
            {{ completeButtonName }}
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
  props: ["tasks"],
  data() {
    return {
        completeButtonName : "Check all",
        completeSwitchStatus : true,
        color: 'info',
        newTask: ""
    };
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
    },
    switchAllTask: function() {
      this.tasks.forEach(task => (task.complete = this.completeSwitchStatus));
      this.color = this.color !=="info" ? "info" : "secondary";
      this.completeButtonName = this.completeButtonName !== "Check all" ? "Check all" : "Uncheck all";
      this.completeSwitchStatus = !this.completeSwitchStatus;
    },
    deleteTask: function(id) {
      this.tasks = this.tasks.filter(task => task.id !== id);
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

  .task {
    font-size: 1.4em;
    line-height: 1.3em;
    height: 50px;
  }

  button {
    line-height: 1em;
  }
}
</style>
