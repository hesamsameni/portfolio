<template>
  <ul class="space-y-8">
    <li v-for="(job, index) in jobs" :key="job.id">
      <div class="flex items-start gap-4">
        <div class="pt-1.5 flex-shrink-0">
          <span
            class="block w-1.5 h-1.5 rounded-full"
            :class="
              job.end_date === 'Present'
                ? 'current-dot'
                : 'opacity-20 bg-current'
            "
          />
        </div>
        <div class="flex-1 min-w-0">
          <div
            class="flex flex-wrap items-baseline justify-between gap-x-4 gap-y-0.5 mb-1"
          >
            <div class="text-sm">
              <span class="font-semibold">{{ job.company }}</span>
              <span class="opacity-30 mx-1.5">/</span>
              <span class="opacity-60">{{ job.position }}</span>
            </div>
            <div class="font-mono text-xs opacity-30 flex-shrink-0">
              {{ job.start_date }} &mdash; {{ job.end_date }}
            </div>
          </div>
          <p class="font-mono text-xs opacity-30 mb-3">
            {{
              job.end_date === "Present"
                ? computeDuration(job.start_date)
                : job.duration
            }}
          </p>
          <div class="flex flex-wrap gap-1.5">
            <span
              v-for="skill in job.skills"
              :key="skill"
              class="skill-tag text-xs px-2 py-0.5"
            >
              {{ skill }}
            </span>
          </div>
        </div>
      </div>
      <hr v-if="index < jobs.length - 1" class="job-divider mt-8 border-t" />
    </li>
  </ul>
</template>

<script setup>
const monthNames = [
  "January",
  "February",
  "March",
  "April",
  "May",
  "June",
  "July",
  "August",
  "September",
  "October",
  "November",
  "December",
];

function computeDuration(startDateStr) {
  const [monthName, year] = startDateStr.split(" ");
  const startMonth = monthNames.indexOf(monthName);
  const startYear = parseInt(year, 10);
  const now = new Date();
  const endMonth = now.getMonth();
  const endYear = now.getFullYear();

  let months = (endYear - startYear) * 12 + (endMonth - startMonth);
  const years = Math.floor(months / 12);
  months = months % 12;

  if (years === 0) return `${months} month${months !== 1 ? "s" : ""}`;
  if (months === 0) return `${years} year${years !== 1 ? "s" : ""}`;
  return `${years} year${years !== 1 ? "s" : ""}, ${months} month${months !== 1 ? "s" : ""}`;
}

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
