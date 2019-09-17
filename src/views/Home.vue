<template>
  <div class="home">
    <div class="col-sm-6 offset-sm-3">
      <h1>Here you type you task</h1>
      <div class="tasks">
        <div v-for="task in tasks" v-bind:key="task.id">
          {{ task.content }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  el: "#home",
  data() {
    return {
      tasks: [
        {
          id: 1,
          content: "Finish to do list app"
        }
      ]
    };
  }
};
</script>

<style lang="sass">

</style>

