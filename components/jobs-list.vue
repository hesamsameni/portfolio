<template>
  <div v-if="pending">Loading...</div>
  <div v-else-if="error">Something went wrong</div>
  <div v-else>
    <ul class="grid grid-cols-1 gap-4">
      <li
        v-for="job in jobs"
        :key="job.id"
        class="rounded-sm p-4 font-mono job"
        :class="{ 'current-job': job.end_date === 'Present' }"
      >
        <div v-if="job.end_date === 'Present'" class="font-bold">
          Current Job
        </div>
        <div class="flex items-center justify-between text-sm">
          <div class="font-semibold">{{ job.company }}</div>
          <div>{{ job.position }}</div>
        </div>

        <p class="text-sm">
          {{ job.duration }}
        </p>
        <div class="skills mt-5">
          <span
            v-for="skill in job.skills"
            :key="skill"
            class="inline-block rounded-full px-2 py-1 text-xs font-semibold mr-2"
          >
            {{ skill }}
          </span>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
const jobs = [
  {
    id: 1,
    company: "Mercedes-Benz.io",
    logo: "https://www.mercedes-benz.io/wp-content/uploads/2021/05/cropped-favicon-192x192.png",
    position: "Frontend Developer",
    employment_type: "Full-time",
    start_date: "March 2022",
    end_date: "Present",
    duration: "2 years, 11 months",
    location: "Portugal",
    skills: ["TypeScript", "JavaScript", "Vue.js", "Nuxt.js"],
  },
  {
    id: 2,
    company: "Cosmos Pics",
    logo: "https://cosmospics.com/logo.png",
    position: "Senior Frontend Developer",
    employment_type: "Freelance",
    start_date: "April 2021",
    end_date: "March 2022",
    duration: "1 year",
    location: "Lisbon, Portugal",
    skills: ["TypeScript", "JavaScript", "Vue.js"],
  },
  {
    id: 3,
    company: "VGANG",
    logo: "https://vgang.io/assets/images/logo.png",
    position: "Lead Frontend Developer",
    employment_type: "Full-time",
    start_date: "January 2020",
    end_date: "March 2022",
    duration: "2 years, 3 months",
    location: "Lisbon, Portugal",
    skills: ["TypeScript", "JavaScript", "Angular"],
  },
  {
    id: 4,
    company: "TiaraUXD",
    logo: "https://tiarauxd.com/logo.png",
    position: "Frontend Developer",
    employment_type: "Full-time",
    start_date: "December 2019",
    end_date: "July 2021",
    duration: "1 year, 8 months",
    location: "Tehran Province, Iran",
    skills: ["TypeScript", "JavaScript", "CSS3"],
  },
  {
    id: 5,
    company: "Bonyadvokala",
    logo: "https://bonyadvokala.com/logo.png",
    position: "React Native Developer",
    employment_type: "Contract",
    start_date: "February 2019",
    end_date: "December 2019",
    duration: "11 months",
    location: "Tehran Province, Iran",
    skills: ["TypeScript", "JavaScript", "React Native"],
  },
];
</script>
