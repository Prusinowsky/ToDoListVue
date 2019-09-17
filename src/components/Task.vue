<template>
  <div class="task">
    <b-form-checkbox class="d-inline" size="lg" v-model="task.complete">
      <div :class="{ completed: task.complete }">
        {{ task.content }}
      </div>
    </b-form-checkbox>
    <b-button
      class="d-inline float-right"
      pill
      variant="outline-secondary"
      size="sm"
      @click="$emit('deleteTask', task.id)"
      >&times;</b-button
    >
  </div>
</template>

<script>
export default {
  name: "Task",
  props: ["task"],
  methods: {}
};
</script>

<style lang="scss">
.completed {
  text-decoration: line-through;
}
</style>
