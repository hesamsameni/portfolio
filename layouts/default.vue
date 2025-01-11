<template>
  <div class="container mx-auto max-w-7xl">
    <header class="flex justify-between items-center mt-5">
      <div>
        <nuxt-link to="/" class="text-xl font-semibold p-5 hover:text-gray-500">
          Hesam Sameni
        </nuxt-link>
      </div>
      <Menu />
    </header>
    <main class="p-5">
      <slot />
    </main>
  </div>
</template>

<script setup>
useHead({
  link: [
    {
      rel: "preconnect",
      href: "https://fonts.googleapis.com",
    },
    {
      rel: "stylesheet",
      href: "https://fonts.googleapis.com/css2?family=Roboto&display=swap",
      crossorigin: "",
    },
  ],
});
</script>

<style>
body {
  font-family: "Roboto";
}
</style>
