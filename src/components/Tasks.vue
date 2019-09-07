<template>
  <div>
    <div class="tasks">
      <template v-if="tasks.length">
        <Task
          v-for="task in tasks"
          :key="task.name"
          :task="task"
          @taskDeleted="taskDeleted"
          @taskStateChange="taskStateChange"
        ></Task>
      </template>
      <template v-else>
        <h3>Sua vida está em dia! :)</h3>
      </template>
    </div>
  </div>
</template>

<script>
import Task from "@/components/Task";

export default {
  name: "Tasks",
  components: {
    Task
  },
  methods: {
    taskDeleted(task) {
      this.$emit('taskDeleted', task);
    },
    taskStateChange(task) {
      this.$emit('taskStateChange', task);
    }
  },
  props: {
    tasks: { type: Array, required: true }
  }
}
</script>

<style scoped>
  .tasks {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
  }

  h3 {
    color: green;
    font-size: 2em;
  }

</style>
