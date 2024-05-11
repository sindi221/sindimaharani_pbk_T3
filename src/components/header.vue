<script setup>
const props = defineProps(["getTasks"]);
</script>

<template>
  <header class="p-5 mb-4 mt-8 rounded-3 text-center">
    <h1><b>"Hey! Ready to tackle your to-do list?"</b></h1>
    <p>list {{ props.getTasks }} </p>
  </header>
</template>