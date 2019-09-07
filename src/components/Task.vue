<template>
  <div
    class="task"
    @click="stateChange"
    :class="stateClass">
    <span
      class="close"
      @click="taskDelete">x</span>
    <h2>{{ task.name }}</h2>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: {
    task: { type: Object, required: true }
  },
  methods: {
    taskDelete() {
      this.$emit('taskDeleted', this.task);
    },
    stateChange() {
      this.$emit('taskStateChange', this.task);
    }
  },
  computed: {
    stateClass() {
      return {
        pending: this.task.pending,
        done: !this.task.pending
      }
    }
  }
}
</script>

<style scoped>
  .task {
    display: flex;
    justify-content: center;
    align-items: center;
    user-select: none;
    background: aliceblue;
    border-radius: 0.5em;
    padding: 0 2em;
    margin: 1em;
    font-size: 0.7em;
    color: white;
    position: relative;
    font-family: 'Manjari', sans-serif;
  }

  .close {
    position: absolute;
    top: 0.5em;
    right: 0.5em;
    font-weight: bold;
  }

  h2 {
    font-weight: 200;
  }

  .pending {
    background: red;
  }

  .done {
    background: green;
    text-decoration: line-through;
  }
</style>
