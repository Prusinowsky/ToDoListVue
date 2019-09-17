<template>
  <div class="task">
    <div>
      <b-form-checkbox class="d-inline" size="lg" v-model="task.complete">
      </b-form-checkbox>
      <div class="d-inline">
        <div class="d-inline"
          v-if="!edit"
          :class="{ completed : task.complete }"
          @click="edit = 'true'"
        >
          {{ task.content }}
        </div>
        <label>
          <input
            v-if="edit"
            type="text"
            v-model="task.content"
            @keyup.enter="doneEdit"
          />
        </label>

        <b-button
          class="d-inline float-right"
          pill
          variant="outline-secondary"
          size="sm"
          @click="$emit('deleteTask', task.id)"
          >&times;</b-button
        >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: ["task"],
  data() {
    return {
      edit: false
    };
  },
  watch: {
    'task.complete': function () {
      this.$emit('completeTask', {id: this.$props.task.id ,status: this.$props.task.complete});
    }
  },
  methods: {
    doneEdit: function () {
      this.edit = !this.edit;
      this.$emit('editTask', {id: this.$props.task.id , newValue: this.$props.task.content});
    }
  }
};
</script>

<style lang="scss">
.completed {
    color: #aaa;
  text-decoration: line-through;
}
</style>
