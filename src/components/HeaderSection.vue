<template>
  <header class="header">
    <h1>{{ title }}</h1>
    <p>{{ subtitle }}</p>
  </header>
</template>

<script setup>
defineProps({
  title: String,
  subtitle: String
})
</script>

<style scoped>
.header {
  text-align: center;
  margin-bottom: 20px;
}
</style>
