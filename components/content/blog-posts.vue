<template>
  <section id="blog" class="not-prose font-mono">
    <div class="column text-gray-400 text-sm">
      <div>date</div>
      <div>title</div>
    </div>
    <ul>
      <li v-for="blog in blogPosts" :key="blog._path">
        <NuxtLink
          :to="blog._path"
          class="column group hover:bg-gray-100 dark:hover:bg-gray-800"
        >
          <div class="text-gray-500">
            {{ blog._dir }}
          </div>
          <div>{{ blog.title }}</div>
        </NuxtLink>
      </li>
    </ul>
  </section>
</template>
  
  <script setup>
const { data: blogPosts } = await useAsyncData("blog-list", () =>
  queryContent("/blog")
    .where({ _path: { $ne: "/blog" } })
    .only(["title", "_path", "_dir"])
    .find()
);

useHead({
  titleTemplate: "Blog Page",
});
</script>
  

<style scoped>
.column {
  @apply flex items-center space-x-8 py-2 border-b border-gray-200 dark:border-gray-700;
}
</style>