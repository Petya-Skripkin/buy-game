<template>
  <h3 class="counter">
    Your {{name}}: {{count}}
  </h3>
</template>

<script>
export default {
  props: {
    name: String,
    count: Number,
  }
}
</script>

<style scoped>
  .counter {
    font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
    font-style: italic;
  }
</style>