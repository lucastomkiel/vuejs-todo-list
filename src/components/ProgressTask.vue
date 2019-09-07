<template>
  <div class="progress">
    <div class="value">
      <span>
        {{ progress }}%
      </span>
    </div>
    <div
      class="bar"
      :style="{ width: progress + '%'}"
    ></div>
  </div>
</template>

<script>
  export default {
    name: "ProgressTask",
    props: {
      progress: { type: Number, default: 0 }
    }
  }
</script>

<style scoped>
  .progress {
    border: 0.1em solid burlywood;
    padding: 0.5em;
    margin: 0em 5em;
    border-radius: 0.5em;
    position: relative;
  }

  .value {
    font-family: 'Manjari', sans-serif;
    text-align: center;
    position: relative;
    z-index: 2;
    font-weight: bold;
    font-size: 1.2em;
    color: darkgrey;
  }

  .bar {
    background: lightgreen;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
    border-radius: 0.5em;
  }
</style>
