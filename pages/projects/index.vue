<template>
  <section>
    <p class="text-xs font-mono uppercase tracking-widest opacity-30 mb-8">
      Projects
    </p>

    <ul class="space-y-8">
      <li v-for="(project, index) in projects" :key="project.id">
        <div class="flex items-start gap-4">
          <div class="pt-1.5 flex-shrink-0">
            <span
              class="block w-1.5 h-1.5 rounded-full"
              :class="project.live ? 'current-dot' : 'opacity-20 bg-current'"
            />
          </div>
          <div class="flex-1 min-w-0">
            <div
              class="flex flex-wrap items-baseline justify-between gap-x-4 gap-y-0.5 mb-1"
            >
              <div class="text-sm font-semibold">{{ project.name }}</div>
              <div class="font-mono text-xs opacity-30 flex-shrink-0">
                {{ project.year }}
              </div>
            </div>
            <p class="text-sm opacity-60 mb-3 leading-relaxed">
              {{ project.description }}
            </p>
            <div class="flex flex-wrap gap-1.5 mb-3">
              <span
                v-for="tech in project.stack"
                :key="tech"
                class="skill-tag text-xs px-2 py-0.5"
              >
                {{ tech }}
              </span>
            </div>
            <div class="flex gap-4">
              <a
                v-if="project.github"
                :href="project.github"
                target="_blank"
                rel="noopener noreferrer"
                class="font-mono text-xs opacity-40 hover:opacity-100 transition-opacity"
              >
                github &nearr;
              </a>
              <a
                v-if="project.live"
                :href="project.live"
                target="_blank"
                rel="noopener noreferrer"
                class="font-mono text-xs opacity-40 hover:opacity-100 transition-opacity"
              >
                live &nearr;
              </a>
            </div>
          </div>
        </div>
        <hr
          v-if="index < projects.length - 1"
          class="job-divider mt-8 border-t"
        />
      </li>
    </ul>
  </section>
</template>

<script setup>
useHead({ titleTemplate: "Projects — Hesam Sameni" });

// Add your projects here — each entry will appear as a card on the page
const projects = [
  {
    id: 2,
    name: "Musicly",
    description:
      "Social platform for music lovers to share and discover tracks.",
    year: "2025",
    stack: ["Vue.js", "TypeScript", "Supabase", "PostgreSQL"],
    github: "https://github.com/hesamsameni/musicly-documents",
    live: "https://musicly.me",
  },
  {
    id: 3,
    name: "Lumiar",
    description: "A credit based platform to generate or edit images with AI.",
    year: "2026",
    stack: [
      "Vue.js",
      "TypeScript",
      "Supabase",
      "PostgreSQL",
      "OpenAI",
      "OpenRouter",
    ],
    github: "https://github.com/hesamsameni/Lumiar",
    live: "https://lumiar.site",
  },
  {
    id: 4,
    name: "Meloria",
    description:
      "Personal second brain to store your movies, books, shows, that knows your taste and suggests you relative content powered by AI",
    year: "2026",
    stack: ["Nuxt", "Nodejs", "Supabase", "OpenAI", "PostHog"],
    github: "https://github.com/hesamsameni/Meloria-app",
    live: "https://meloria-app.com",
  },
  {
    id: 5,
    name: "Roomie",
    description:
      "Expense tracker for roommates and couples to manage shared bills and expenses.",
    year: "2025",
    stack: ["Nuxt", "Nodejs", "Supabase"],
    github: "https://github.com/hesamsameni/roomie-app",
    live: "https://www.roomie-app.site/",
  },
  {
    id: 6,
    name: "Portfolio",
    description: "Personal portfolio site built with Nuxt.js and Tailwind CSS.",
    year: "2024",
    stack: ["Nuxt.js", "Vue.js", "TypeScript", "Tailwind CSS"],
    github: "https://github.com/hesamsameni/portfolio",
    live: "https://hesamsameni.site/",
  },
];
</script>
