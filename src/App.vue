<template>
  <div id="app">
    <h1>Tarefas</h1>
    <ProgressTask :progress="progress"></ProgressTask>
    <NewTask @taskAdded="addTask"></NewTask>
    <Tasks
      :tasks="tasks"
      @taskDeleted="removeTask"
      @taskStateChange="stateChangeTask"></Tasks>
  </div>
</template>

<script>
import Tasks from "@/components/Tasks";
import NewTask from "@/components/NewTask";
import ProgressTask from "@/components/ProgressTask";

export default {
  name: 'app',
  components: {
    Tasks,
    NewTask,
    ProgressTask
  },
  computed: {
    progress() {
      const total = this.tasks.length;
      const done = this.tasks.filter(t => !t.pending).length;
      return Math.round(done / total * 100) || 0;
    }
  },
  watch: {
    tasks: {
      deep: true,
      handler() {
        localStorage.setItem('tasks', JSON.stringify(this.tasks));
      }
    }
  },
  data() {
    return {
      tasks: []
    }
  },
  created() {
    const json = localStorage.getItem('tasks');
    this.tasks = JSON.parse(json) || [];
  },
  methods: {
    addTask(task) {
      this.tasks.push({
        name: task.name,
        pending: task.pending || true
      });
    },
    removeTask(task) {
      const taskId = this.tasks.indexOf(task);
      this.tasks.splice(taskId, 1);
    },
    stateChangeTask(task) {
      const taskId = this.tasks.indexOf(task);
      this.tasks[taskId].pending = !this.tasks[taskId].pending;
    }
  }
}
</script>

<style>
  body {
    background: floralwhite;
  }

  h1, h3 {
    font-family: 'Livvic', sans-serif;
  }

  h1 {
    color: darkgrey;
    text-align: center;
  }
</style>
