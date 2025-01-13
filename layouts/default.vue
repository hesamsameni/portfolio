<template>
  <div class="container mx-auto max-w-7xl">
    <header class="flex justify-between items-start items-center mt-5 p-10">
      <div class="flex items-center">
        <div>
          <NuxtLink
            to="/"
            class="text-sm font-semibold hover:bg-gray-200 dark:hover:bg-gray-700 md:text-xl"
          >
            Hesam Sameni
          </NuxtLink>
        </div>

        <Menu />
      </div>

      <ClientOnly>
        <ColorModeSelector />
      </ClientOnly>
    </header>
    <main class="p-10">
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
