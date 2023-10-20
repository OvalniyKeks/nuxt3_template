<script setup lang="ts">
const { data } = await useFetch('/api/hello')
</script>

<template>
  <div>
    Hello World
    {{ data }}
  </div>
</template>
