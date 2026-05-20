<template>
  <div class="scroller mt-10">
    <div class="scroll-clip">
      <div class="tag-list">
        <div v-for="n in 2" :key="n" class="tech-group">
          <div v-for="tech in allTech" :key="`${tech}-${n}`" class="tech-card-container" @mouseenter="activeTech = tech"
            @mouseleave="activeTech = null" @mousemove="updateTooltip">
            <span class="tag">
              <div class="tag-content">
                <img :src="getTechIconUrl(tech)" :alt="tech" class="tag-icon-img" @error="handleImageError" />
                <span class="tag-name">{{ tech }}</span>
              </div>
            </span>
          </div>
        </div>

        <Teleport to="body">
          <div v-if="activeTech" class="tech-tooltip" :style="tooltipStyle">
            {{ getTech(activeTech).knowledge }}
          </div>
        </Teleport>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { techIcons } from "../data/techIcons";
const activeTech = ref(null);
const tooltipStyle = ref({});

const allTech = ref([
  "C", "C++", "PHP", "Laravel", "Flutter", "JavaScript", "Node.js", "Express",
  "Firebase", "SQL", "HTML5", "CSS3", "Tailwind", "Bootstrap", "React", "Vue",
  "Git", "GitHub", "Cloudinary", "Stripe", "VSCode", "Android Studio", "Figma",
  "Postman", "Render", "Railway", "Netlify", "Neon", "Google", "ChatGPT", "DeepSeek", "Gemini"
]);

const updateTooltip = (e) => {
  let top = e.clientY + 12;
  let left = e.clientX + 12;

  // Get tooltip width and height after it renders
  setTimeout(() => {
    const tooltip = document.querySelector('.tech-tooltip');
    if (tooltip) {
      const tooltipRect = tooltip.getBoundingClientRect();
      const windowWidth = window.innerWidth;
      const windowHeight = window.innerHeight;

      // Adjust if off-screen right
      if (left + tooltipRect.width > windowWidth - 10) {
        left = e.clientX - tooltipRect.width - 12;
      }

      // Adjust if off-screen bottom
      if (top + tooltipRect.height > windowHeight - 10) {
        top = e.clientY - tooltipRect.height - 12;
      }

      // Adjust if off-screen left
      if (left < 10) {
        left = 10;
      }

      // Adjust if off-screen top
      if (top < 10) {
        top = 10;
      }

      tooltipStyle.value = {
        position: "fixed",
        top: top + "px",
        left: left + "px",
        zIndex: 999999,
        maxWidth: "280px",
        whiteSpace: "normal",
        wordWrap: "break-word"
      };
    }
  }, 10);

  // Initial position
  tooltipStyle.value = {
    position: "fixed",
    top: top + "px",
    left: left + "px",
    zIndex: 999999,
    maxWidth: "280px",
    whiteSpace: "normal",
    wordWrap: "break-word"
  };
};

// Get icon URL from techIcons
const getTechIconUrl = (tech) => {
  return techIcons[tech]?.url || "";
};

const getTech = (techName) => {
  return techIcons[techName] || { knowledge: "No information available" };
};

// Handle image load errors - show fallback
const handleImageError = (event) => {
  event.target.style.display = "none";
  // Optional: show a fallback text instead of broken image
  event.target.nextSibling?.classList.add("no-icon");
};
</script>

<style>
.tech-tooltip {
  background: rgba(10, 10, 30, 0.95);
  color: white;
  padding: 10px;
  width: 250px;
  border-radius: 10px;
  font-size: 0.9rem;
  line-height: 1.4;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
  pointer-events: none;
  word-wrap: break-word;
  white-space: normal;
}

.scroller {
  position: relative;
  max-width: 1300px;
}

.scroll-clip {
  overflow: hidden;
  mask-image: linear-gradient(to right,
      transparent,
      black 10%,
      black 90%,
      transparent);
}

.tag-list {
  display: flex;
  gap: 1rem;
  width: max-content;
  animation: scroll 40s linear infinite;
}

.scroller:hover .tag-list {
  animation-play-state: paused;
}

.tech-group {
  display: flex;
  gap: 1rem;
  flex-shrink: 0;
}

@keyframes scroll {
  to {
    transform: translateX(calc(-60% - 0.5rem));
  }
}

/* ================= TAG CARD ================= */

.tech-card-container {
  position: relative;
  z-index: 1;
  width: 70px;
  height: 70px;
  flex-shrink: 0;
}

.tag {
  width: 100%;
  height: 100%;
  border-radius: 10px;
  background: rgba(255, 255, 255, 0.059);

  display: flex;
  align-items: center;
  justify-content: center;

  transition: background-color 0.2s ease, transform 0.3s ease;
}

.tech-card-container:hover .tag {
  background: rgba(255, 255, 255, 0.2);
  transform: translateY(5px);
}

/* ================= CONTENT ================= */

.tag-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.25rem;
}

.tag-icon {
  font-size: 24px;
  transition: transform 0.3s ease;
}

.tag-icon-img {
  width: 24px;
  height: 24px;
  transition: transform 0.3s ease;
  z-index: 1;
}

.tag-name {
  font-size: 0.75rem;
  font-weight: 500;
  color: #ccc;
  text-align: center;
}

/* ================= HOVER INFO ================= */

.tag-info {
  position: absolute;
  top: 100%;
  left: 50%;
  width: 200px;

  transform: translate(-50%, -10px);
  opacity: 0;
  pointer-events: none;

  background: rgba(10, 10, 30, 0.95);
  color: white;
  padding: 10px;
  border-radius: 10px;
  text-align: center;

  transition: opacity 0.3s ease, transform 0.3s ease;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
}

.tag-info p {
  margin: 0;
  font-size: 0.8rem;
  line-height: 1.3;
}

.tech-card-container:hover .tag-info {
  opacity: 1;
  transform: translate(-50%, 5px);
}
</style>
