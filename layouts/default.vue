<template>
  <div class="container mx-auto max-w-2xl px-6">
    <header
      class="flex justify-between items-center py-7 border-b theme-border"
    >
      <div class="flex items-center gap-8">
        <NuxtLink
          to="/"
          class="font-mono text-sm font-semibold tracking-tight hover:opacity-70 transition-opacity"
        >
          Hesam Sameni
        </NuxtLink>
        <Menu />
      </div>
      <ClientOnly>
        <ColorModeSelector />
      </ClientOnly>
    </header>
    <main class="py-12">
      <slot />
    </main>
    <footer class="py-6 border-t theme-border">
      <span class="font-mono text-xs opacity-30"
        >built with nuxt.js &middot; {{ new Date().getFullYear() }}</span
      >
    </footer>
  </div>
</template>

<script setup>
useHead({
  link: [
    { rel: "preconnect", href: "https://fonts.googleapis.com" },
    { rel: "preconnect", href: "https://fonts.gstatic.com", crossorigin: "" },
    {
      rel: "stylesheet",
      href: "https://fonts.googleapis.com/css2?family=JetBrains+Mono:ital,wght@0,400;0,500;0,600;0,700;1,400&display=swap",
      crossorigin: "",
    },
  ],
});
</script>

<style>
body {
  font-family: "JetBrains Mono", "Fira Code", "Cascadia Code", monospace;
  font-size: 14px;
  line-height: 1.75;
}
</style>
