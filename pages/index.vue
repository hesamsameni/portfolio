<template>
  <div class="space-y-10">
    <section class="space-y-5">
      <div>
        <h1 class="text-xl font-semibold tracking-tight mb-1">Hesam Sameni</h1>
        <p class="text-sm opacity-40 font-mono">
          Frontend Developer &mdash; Lisbon, Portugal
        </p>
      </div>

      <div class="space-y-3 text-sm leading-relaxed opacity-75 max-w-lg">
        <p>
          I build web interfaces with a focus on
          <span class="font-medium opacity-100">Vue.js</span>,
          <span class="font-medium opacity-100">Nuxt.js</span>, and
          <span class="font-medium opacity-100">TypeScript</span>. Currently at
          <span class="font-medium opacity-100">Mercedes-Benz.io</span>, working
          on frontend solutions that balance design and performance.
        </p>
        <p>
          Beyond the frontend, I integrate AI into production apps, working
          directly with
          <span class="font-medium opacity-100">OpenAI</span>,
          <span class="font-medium opacity-100">OpenRouter</span>, and
          <span class="font-medium opacity-100">Google APIs</span>, optimising
          token usage, and building with agentic workflows. On the data side, I
          design and tune queries in
          <span class="font-medium opacity-100">Supabase</span> and
          <span class="font-medium opacity-100">PostgreSQL</span>.
        </p>
        <p>
          I care about clean code, good UX, accessibility, and developer
          experience. Outside work: video games, bike rides, and
          over-engineering my coffee setup.
        </p>
      </div>
    </section>

    <section class="space-y-2">
      <p class="text-xs opacity-30 font-mono uppercase tracking-widest mb-4">
        Stack
      </p>
      <div class="flex flex-wrap gap-2">
        <span
          v-for="tech in stack"
          :key="tech"
          class="skill-tag text-xs px-2 py-0.5 font-mono"
        >
          {{ tech }}
        </span>
      </div>
    </section>
  </div>
</template>

<script setup>
useHead({ titleTemplate: "Hesam Sameni" });

const stack = [
  "TypeScript",
  "JavaScript",
  "Vue.js",
  "Nuxt.js",
  "CSS",
  "SCSS",
  "Tailwind",
  "OpenAI",
  "OpenRouter",
  "Google APIs",
  "Supabase",
  "PostgreSQL",
];
</script>
