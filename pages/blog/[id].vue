<template>
  <div>
    <h1>Post id is {{ route.params.id }}</h1>
  </div>
</template>

<script setup>
const route = useRoute();

useHead({
  titleTemplate: `Blog Post - ${route.params.id}`,
});
</script>
