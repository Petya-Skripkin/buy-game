<template>
  <button>
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'my-button',
}
</script>

<style scoped>
  button {
    border-radius: 10px;
    cursor: pointer;
  }
</style>