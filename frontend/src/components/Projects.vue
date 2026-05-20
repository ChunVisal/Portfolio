<template>
  <section class="projects-section px-5 sm:px-10 py-10">
    <h1 class="projects-title">
      <span>My, </span>
      <span>Projects</span>
      <span> & </span>
      <span>Tech Stack</span>
    </h1>

    <div class="projects-grid">
      <div v-for="(project, index) in projects" :key="project.id" class="project-card-wrapper"
        @mouseenter="!isMobile ? (active = index) : null"
        @mouseleave="() => { if (!isMobile) { active = null; handleMouseLeave(index); } }"
        @mousemove="(e) => !isMobile && handleMouseMove(e, index)" :style="{ transform: cardTransforms[index] }">
        <RouterLink :to="`/project/${project.id}`" class="interactive-card"
          :style="{ transform: cardTransforms[index] }">
          <span class="project-status">
            <VueFeather type="circle" :fill="project.status === 'Completed' ? 'green' : 'yellow'"
              :stroke="project.status === 'Completed' ? 'green' : 'yellow'" size="12" />
            {{ project.status }}
          </span>
          <img :src="project.img" alt="Projects" class="card-image" />
        </RouterLink>

        <div class="panel" :class="{ 'panel-mobile-visible': isMobile }" v-if="active === index || isMobile">
          <h2 class="project-title">{{ project.title }}</h2>
          <p class="project-description">{{ project.description }}</p>
          <ul class="project-tech-stack flex flex-wrap gap-2 mt-3 justify-center md:justify-start">
            <li v-for="tech in project.tech" :key="tech"
              class="inline-flex items-center justify-center gap-1.5 px-3 py-1 bg-white/10 rounded-full text-xs">
              <img :src="getTechIconUrl(tech)" class="w-4 h-4 object-contain" :alt="tech" />
              <span>{{ tech }}</span>
            </li>
          </ul>
        </div>
      </div>
    </div>

    <Teackstack />
  </section>
</template>

<script setup>
import { ref, onMounted } from "vue";
import Teackstack from "../components/Teackstack.vue";
import { techIcons } from "../data/techIcons";

const apexmotor = "https://res.cloudinary.com/dexr27qho/image/upload/v1778567949/apexmotor_rvjahl.png";
const venubooking = "https://res.cloudinary.com/dexr27qho/image/upload/v1778568319/venubooking_flkkd6.png";
const portfolio = "https://res.cloudinary.com/dexr27qho/image/upload/v1778568375/portfolio_kh7emx.png";

const projects = [
  {
    id: 1,
    img: apexmotor,
    title: "ApexMotor",
    description:
      "A full-stack car marketplace built with a component-based UI, real-time data handling, and authentication for user actions like listing and purchasing vehicles.",
    tech: ["React", "Tailwind", "Firebase"],
    status: "Completed",
  },
  {
    id: 2,
    img: venubooking,
    title: "VenuBooking",
    description:
      "An event ticket booking system with RESTful APIs, backend logic for reservations, and a relational database to manage users, events, and transactions.",
    tech: ["React", "Node.js", "SQL", "Tailwind",],
    status: "Completed",
  },
  {
    id: 3,
    img: portfolio,
    title: "Portfolio",
    description:
      "A performance-optimized personal portfolio built with modern animations, responsive layouts, and reusable components to showcase projects and skills.",
    tech: ["Vue", "GSAP", "Tailwind"],
    status: "Completed",
  },
];

const active = ref(null);
const isMobile = ref(false);

const checkMobile = () => {
  isMobile.value = window.innerWidth < 640;
};

// Add this function
const getTechIconUrl = (tech) => {
  return techIcons[tech]?.url || "";
};

onMounted(() => {
  checkMobile();
  window.addEventListener("resize", checkMobile);
});

const cardTransforms = ref(projects.map(() => ""));
const maxRotation = 20;

const handleMouseMove = (e, index) => {
  if (isMobile.value) return;

  const rect = e.currentTarget.getBoundingClientRect();
  const x = e.clientX - rect.left;
  const y = e.clientY - rect.top;
  const centerX = rect.width / 2;
  const centerY = rect.height / 2;

  const rotateX = (centerY - y) / (rect.height / (2 * maxRotation));
  const rotateY = (x - centerX) / (rect.width / (2 * maxRotation));

  cardTransforms.value[
    index
  ] = `perspective(1000px) rotateX(${rotateX}deg) rotateY(${rotateY}deg) scale(1.05)`;
};

const handleMouseLeave = (index) => {
  if (isMobile.value) return;

  cardTransforms.value[
    index
  ] = `perspective(1000px) rotateX(0deg) rotateY(0deg) scale(1)`;
};
</script>

<style scoped>
.projects-section {
  display: flex;
  flex-direction: column;
  position: relative;
  width: 100%;
  margin: 0 auto;
  max-width: 1300px;
}

.project-card-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;

  border-radius: 10px;
  position: relative;
  isolation: isolate;
}

.project-card-wrapper:hover {
  z-index: 100;
}

.scroller {
  position: relative;
  z-index: 1;
}

.projects-grid {
  margin-top: 2rem;
  display: grid;
  gap: 2rem;
  /* mobile 2 and pc 3 */
  grid-template-columns: repeat(auto-fit, minmax(230px, 1fr));
}

.interactive-card {
  width: 100%;
  height: 200px;
  overflow: hidden;
  transform-style: preserve-3d;
  transform: perspective(1000px) rotateX(0deg) rotateY(0deg);
  transition: transform 0.25s ease-out;
  cursor: pointer;
}

.card-image {
  width: 100%;
  height: 100%;
  object-fit: contain;
  transition: filter 0.25s ease;
}

.tech-icon-img {
  width: 20px;
  height: 20px;
  object-fit: contain;
}

/* hover */
.interactive-card:hover .card-image {
  filter: drop-shadow(0 0 12px rgba(213, 213, 255, 0.189));
}

.projects-title :nth-child(2),
:nth-child(4) {
  font-weight: 700;
  letter-spacing: -0.02em;
  background: linear-gradient(135deg, #667eea, #764ba2);
  background-clip: text;
  -webkit-text-fill-color: transparent;
}

.item {
  position: relative;
  width: 200px;
  padding: 10px;
  background: #222;
  color: white;
  margin-bottom: 10px;
}

.panel {
  position: absolute;
  top: 100%;
  padding: 10px;
  white-space: nowrap;
  transform: translateY(10px);
  animation: slide 0.2s ease;
  background: rgba(45, 45, 45, 0.626);
  backdrop-filter: blur(2px);
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  white-space: normal;
  word-wrap: break-word;
  z-index: 9999 !important;
  border-radius: 10px;
}

@keyframes slide {
  from {
    opacity: 0;
    transform: translateY(0);
  }

  to {
    opacity: 1;
    transform: translateY(10px);
  }
}

/* project-status at right top relative */
.project-status {
  position: absolute;
  display: flex;
  align-items: center;
  /* vertical center */
  justify-content: center;
  gap: 5px;
  top: 10px;
  right: 10px;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(2px);
  color: white;
  padding: 0.2rem 0.5rem;
  border-radius: 0.25rem;
  font-size: 0.75rem;
  font-weight: 500;
  z-index: 20;
}

.project-title {
  font-size: 1.4rem;
  font-weight: 600;
}

.project-description {
  font-size: 1rem;
  color: #ccc;
}

.project-tech-stack {
  font-size: clamp(0.9rem, 1.4vw, 1rem);
  color: white;
  list-style: none;
  display: flex;
  gap: 0.5rem;
}

.project-tech-stack li {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(2px);
  padding: 0.2rem 0.5rem;
  border-radius: 0.25rem;
  font-size: 0.875rem;
}

/* Mobile Specific Overrides */
@media (max-width: 639px) {
  .project-card-wrapper {
    background: rgba(255, 255, 255, 0.1);
    backdrop-filter: blur(5px);
  }

  .project-card-wrapper {
    align-items: stretch;
  }

  .panel.panel-mobile-visible {
    position: static;
    transform: none;
    animation: none;
    z-index: 9999;
    width: 100%;
    margin-top: -10px;
    padding: 15px 10px;
    border-radius: 10px;
  }

  .panel {
    background: none;
    backdrop-filter: none;
  }

  .interactive-card {
    border-radius: 10px 10px 0 0;
    background: rgba(255, 255, 255, 0.1);
  }

  .project-tech-stack {
    justify-content: center;
  }

  .project-tech-stack li {
    justify-content: center;
  }
}
</style>
