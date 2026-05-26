<template>
  <footer class="portfolio-footer">
    <div class="grid">
      <div class="footer-top-section">
        <div class="footer-col navigate-col">
          <h3 class="col-title">NAVIGATE</h3>
          <ul>
            <li @click="scrollToTop">
              <font-awesome-icon :icon="['fas', 'star']" style="color: darkorchid" class="link-bullet" />
              Home
            </li>
            <li @click="scrollToAbout">
              <font-awesome-icon :icon="['fas', 'star']" style="color: darkorchid" class="link-bullet" />
              About
            </li>
            <li @click="scrollToProjects">
              <font-awesome-icon :icon="['fas', 'star']" style="color: darkorchid" class="link-bullet" />
              Projects
            </li>
            <li>
              <font-awesome-icon :icon="['fas', 'star']" style="color: darkorchid" class="link-bullet" />
              Portfolio
            </li>
            <li @click="NotAvailableYet">
              <font-awesome-icon :icon="['fas', 'star']" style="color: darkorchid" class="link-bullet" />
              Services
            </li>
          </ul>
        </div>

        <div class="footer-col social-col">
          <h3 class="col-title">CONNECT</h3>
          <div class="social-links column-links">
            <a href="https://github.com/ChunVisal" target="_blank">
              <font-awesome-icon :icon="['fab', 'github']" style="color: #c9c9c9" />
              <span>GitHub</span>
            </a>

            <a href="https://www.linkedin.com/in/visal-sal-54b615349" target="_blank">
              <font-awesome-icon :icon="['fab', 'linkedin']" style="color: #c9c9c9" />
              <span>LinkedIn</span>
            </a>

            <a href="https://t.me/joevisal" target="_blank">
              <font-awesome-icon :icon="['fab', 'telegram']" style="color: #c9c9c9" />
              <span>Telegram</span>
            </a>

            <a href="mailto:vsal0882@gmail.com">
              <font-awesome-icon :icon="['fas', 'envelope']" style="color: #c9c9c9" />
              <span>Email</span>
            </a>
          </div>
        </div>
        <div class="footer-col resources-col">
          <h3 class="col-title">RESOURCES</h3>
          <ul>
            <li>
              <a href="/public/ChunVisal_Resume.pdf" download class="flex items-center gap-2">
                <font-awesome-icon :icon="['fas', 'star']" style="color: darkorchid" class="link-bullet" />
                Download CV
              </a>
            </li>
            <li>
              <font-awesome-icon :icon="['fas', 'star']" style="color: darkorchid" class="link-bullet" />
              Website Templates
            </li>
          </ul>
          <div class="comment-form-wrap mt-6">
            <form @submit.prevent="submitComment" class="flex gap-3">
              <input v-model="comment" type="text" placeholder="Comment"
                class="grow border-2 border-gray-500 bg-gray-800/50 py-1 px-5 rounded-sm flex items-center justify-center text-sm" />
              <button type="submit" class="bg-purple-800 px-5 rounded-sm relative text-sm">
                <span v-if="!isLoading">Submit</span>
                <span v-if="isLoading" class="absolute inset-0 flex items-center justify-center">
                  <svg class="animate-spin h-4 w-4 text-white" viewBox="0 0 24 24">
                    <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"
                      fill="none" />
                    <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8v4a4 4 0 00-4 4H4z" />
                  </svg>
                </span>
              </button>
            </form>
          </div>
        </div>
      </div>

      <div class="footer-bottom-section">
        <div class="copyright-area">
          <p class="reserved-text">ALL RIGHTS RESERVED.</p>
          <p class="copyright-main">JOE NARTHAN CODES</p>
        </div>

        <div class="local-time-area flex items-center gap-2">
          <font-awesome-icon :icon="['fas', 'clock']" class="text-purple-300" />
          <span>{{ localTime }}</span>
        </div>

        <div class="domain-link-area flex gap-1 items-center">
          <font-awesome-icon :icon="['fas', 'globe-asia']" class="text-blue-300" />
          <a href="https://chunvisal.pro" target="_blank"
            class="text-md font-bold text-gray-200 hover:text-purple-400 transition-colors flex items-center gap-1">
            HTTPS://CHUNVISAL.PRO
          </a>
        </div>
      </div>
    </div>
  </footer>
</template>

<script setup>
import { ref, onMounted } from "vue";

const localTime = ref("");

onMounted(() => {
  updateTime();
  setInterval(updateTime, 1000);
});

function updateTime() {
  const now = new Date();

  const time = now.toLocaleTimeString("en-US", {
    hour: "2-digit",
    minute: "2-digit",
    second: "2-digit",
    hour12: true,
  });

  // Cambodia = UTC +7 (fixed offset)
  localTime.value = `${time} GMT +7`;
}

const scrollToTop = () => {
  window.scrollTo({
    top: 0,
    behavior: "smooth",
  });
};

const scrollToAbout = () => {
  document.getElementById("about").scrollIntoView({ behavior: "smooth" });
};

const scrollToProjects = () => {
  document.getElementById("projects").scrollIntoView({ behavior: "smooth" });
};

const NotAvailableYet = () => {
  window.alert("I am not available yet");
};
const comment = ref("");
const isLoading = ref(false);

const BACKEND_URL = "https://portfolio-backend-production-85fd.up.railway.app";

const submitComment = async () => {
  if (isLoading.value) return;

  if (!comment.value.trim()) {
    alert("Please type a comment first");
    return;
  }

  isLoading.value = true;

  try {
    const res = await fetch(`${BACKEND_URL}/add-comment`, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({ message: comment.value }),
    });

    if (!res.ok) {
      const errorData = await res
        .json()
        .catch(() => ({ details: "No JSON response body" }));
      alert(
        `Server Failed: ${res.status} - ${errorData.details || errorData.error}`
      );
      return;
    }

    // Success
    alert("Comment submitted successfully!");
    comment.value = "";
  } catch (err) {
    alert("Failed to send to backend. Check console / CORS fix in server.js.");
  } finally {
    isLoading.value = false;
  }
};
</script>

<style scoped>
.portfolio-footer {
  background: linear-gradient(to top, #001f4016 0%, #0000001d 100%);
  color: #fff;
  padding: 3rem 2rem 2rem 2rem;
  min-height: 450px;
  position: relative;
  overflow: hidden;
}

.grid {
  max-width: 1200px;
  margin: 0 auto;
  width: 100%;
}

.footer-top-section {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 3rem;
  margin: 0 auto 3rem;
}

.col-title {
  font-size: 1.25rem;
  font-weight: 700;
  letter-spacing: 2px;
  margin-bottom: 1.5rem;
  background: linear-gradient(135deg, #c9c9c9 0%, #7a38bc 100%);
  background-clip: text;
  -webkit-text-fill-color: transparent;
}

.footer-col ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.footer-col li {
  font-size: 1rem;
  color: #ccc;
  margin-bottom: 0.75rem;
  cursor: pointer;
  transition: color 0.2s;
}

.footer-col li:hover {
  color: #4fc08d;
}

.link-bullet {
  margin-right: 0.5rem;
  font-size: 0.75rem;
}

.column-links {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.social-links a {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  color: #ccc;
  font-size: 1rem;
  text-decoration: none;
  transition: 0.2s;
  white-space: nowrap;
}

.social-links a:hover {
  color: #7a38bc;
}

.social-links svg {
  font-size: 1.2rem;
}

.footer-bottom-section {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.reserved-text {
  font-size: 0.8rem;
  color: #a0a0a0;
  letter-spacing: 1px;
}

.copyright-main {
  font-size: 1.8rem;
  font-weight: 700;
  line-height: 0.9;
  background: linear-gradient(135deg, #c9c9c9 0%, #7a38bc 100%);
  background-clip: text;
  -webkit-text-fill-color: transparent;
  white-space: nowrap;
}

.local-time-area {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.copyright-area p {
  margin: 7px 0;
}

@media (max-width: 640px) {
  .footer-top-section {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    column-gap: 6px;
    row-gap: 16px;
  }

  .footer-top-section>* {
    min-width: 0;
  }

  .footer-bottom-section {
    flex-direction: column;
    align-items: flex-start;
    gap: 1rem;
  }
}
</style>
