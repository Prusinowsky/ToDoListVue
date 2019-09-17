<template>
  <div class="home">

        <tasks v-bind:tasks="tasks"></tasks>

  </div>
</template>

<script>
import Tasks from "../components/Tasks.vue";

export default {
  components: {
    Tasks
  },
  data() {
    return {
      tasks: []
    };
  },
};
</script>

<style lang="scss">

</style>
