<template>
  <div class="new-task">
    <input
      v-model="name"
      @keydown.enter="add"
      placeholder="Nova Tarefa"
      ref="name"
      autofocus
      type="text">
    <button
      @click="add">
      Adicionar
    </button>
  </div>
</template>

<script>
  export default {
    name: "NewTask",
    data() {
      return {
        name: ''
      }
    },
    methods: {
      add() {
        this.$emit('taskAdded', { name: this.name });
        this.name = '';
        this.$refs.name.focus();
      }
    }
  }
</script>

<style scoped>
  .new-task {
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 2em;
  }

  input {
    padding: 0.6em 1.6em;
    border: 0.1em solid burlywood;
    font-family: 'Manjari', sans-serif;
    font-weight: 200;
    border-radius: 0.5em;
    margin: 1em;
    font-size: 1.3em;
  }

  input:focus {
    outline: none;
  }

  button {
    cursor: pointer;
    background: burlywood;
    border: 0.1em solid burlywood;
    padding: 0.6em 1.6em;
    border-radius: 0.5em;
    font-family: 'Manjari', sans-serif;
    font-weight: 200;
    font-size: 1.3em;
  }

  button:focus {
    outline: none;
  }
</style>
