<template>
  <header>
    <img src="../assets/logo.png" width="32" />
    <div>My carrito superpower</div>
    <div>{{ count }}</div>
    <button @click="refresh">Refresh!</button>
  </header>
</template>

<script>
export default {
  props: ["count"],
  emits: ["refresh"],
  methods: {
    refresh() {
      this.$emit('refresh', this.count)
    }
  }
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
}
</style>