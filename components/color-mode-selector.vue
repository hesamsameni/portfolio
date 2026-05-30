<template>
  <button
    @click="toggleMode"
    :title="`Switch to ${nextMode} mode`"
    class="opacity-50 hover:opacity-100 transition-opacity p-1 rounded"
  >
    <svg
      v-if="nextMode === 'light'"
      xmlns="http://www.w3.org/2000/svg"
      width="16"
      height="16"
      viewBox="0 0 24 24"
      fill="none"
      stroke="currentColor"
      stroke-width="2"
      stroke-linecap="round"
      stroke-linejoin="round"
    >
      <circle cx="12" cy="12" r="4" />
      <path
        d="M12 2v2M12 20v2M4.93 4.93l1.41 1.41M17.66 17.66l1.41 1.41M2 12h2M20 12h2M6.34 17.66l-1.41 1.41M19.07 4.93l-1.41 1.41"
      />
    </svg>
    <svg
      v-else
      xmlns="http://www.w3.org/2000/svg"
      width="16"
      height="16"
      viewBox="0 0 24 24"
      fill="none"
      stroke="currentColor"
      stroke-width="2"
      stroke-linecap="round"
      stroke-linejoin="round"
    >
      <path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z" />
    </svg>
  </button>
</template>

<script setup>
const colorMode = useColorMode();

const modes = ["light", "dark"];

const nextMode = computed(() => {
  const currentModeIndex = modes.indexOf(colorMode.preference);
  const nextModeIndex = (currentModeIndex + 1) % modes.length;
  return modes[nextModeIndex];
});

const toggleMode = () => (colorMode.preference = nextMode.value);
</script>
