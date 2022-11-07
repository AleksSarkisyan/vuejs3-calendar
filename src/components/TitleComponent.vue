<script setup>
  defineProps({
    title: {
      type: String,
      required: true
    }
  })
</script>

<template>
  <div class="title">
    <h2>{{ title }}</h2>
  </div>
</template>
  
<style scoped>
  .title {
    text-align: center;
    padding: 30px 0px;
    font-weight: 500;
  }
</style>
