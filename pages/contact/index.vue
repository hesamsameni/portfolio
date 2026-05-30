<template>
  <section class="space-y-10">
    <p class="text-xs font-mono uppercase tracking-widest opacity-30">
      Contact
    </p>

    <p class="text-sm opacity-60 leading-relaxed max-w-sm">
      Open to interesting projects and collaborations. Feel free to reach out.
    </p>

    <div class="space-y-10">
      <div>
        <p class="font-mono text-xs opacity-30 mb-2">email</p>
        <div class="flex items-center gap-4">
          <a
            href="mailto:hesam.sameni@gmail.com"
            class="text-sm opacity-80 hover:opacity-100 transition-opacity"
          >
            hesam.sameni@gmail.com
          </a>
          <button
            @click="copyEmail"
            class="font-mono text-xs px-2 py-0.5 skill-tag opacity-50 hover:opacity-100 transition-opacity"
          >
            {{ copied ? "copied!" : "copy" }}
          </button>
        </div>
      </div>

      <hr class="job-divider border-t" />

      <div class="space-y-6">
        <div v-for="link in socials" :key="link.label">
          <p class="font-mono text-xs opacity-30 mb-1">{{ link.label }}</p>
          <a
            :href="link.url"
            target="_blank"
            rel="noopener noreferrer"
            class="text-sm opacity-70 hover:opacity-100 transition-opacity"
          >
            {{ link.handle }} &nearr;
          </a>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
useHead({ titleTemplate: "Contact — Hesam Sameni" });

const copied = ref(false);

async function copyEmail() {
  await navigator.clipboard.writeText("hesam.sameni@gmail.com");
  copied.value = true;
  setTimeout(() => (copied.value = false), 2000);
}

const socials = [
  {
    label: "github",
    handle: "hesamsameni",
    url: "https://github.com/hesamsameni",
  },
  {
    label: "linkedin",
    handle: "hesamsameni",
    url: "https://www.linkedin.com/in/hesamsameni/",
  },
  {
    label: "instagram",
    handle: "hesamsameni",
    url: "https://www.instagram.com/hesamsameni/",
  },
];
</script>
