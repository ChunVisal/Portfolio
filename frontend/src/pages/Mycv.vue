<script setup>
import { ref, } from 'vue';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
import { techIcons } from '../data/techIcons';

// full screen images
const showPreview = ref(false);

const closePreview = () => {
    showPreview.value = false;
}

const iconKeyMap = {
    HTML: "HTML5",
    CSS: "CSS3",
    JavaScript: "JavaScript",
    React: "React",
    "React.js": "React",
    Vue: "Vue",
    "Vue.js": "Vue",
    Tailwind: "Tailwind",
    "Tailwind CSS": "Tailwind",
    Bootstrap: "Bootstrap",
    "Node.js": "Node.js",
    Express: "Express",
    "Express.js": "Express",
    SQL: "SQL",
    Firebase: "Firebase",
    Postman: "Postman",
    "VS Code": "VSCode",
    Figma: "Figma",
    GitHub: "GitHub",
    Netlify: "Netlify",
    Railway: "Railway"
};

const getTech = (tech) => {
    const key = iconKeyMap[tech] || tech;
    const icon = techIcons[key];
    return {
        name: tech,
        url: icon?.url || "",
        info: icon?.info || "No information available",
        icon: icon?.icon || null,
        color: icon?.color || "text-gray-400"
    };
};

const frontendTech = ["HTML", "CSS", "JavaScript", "React", "Vue", "Tailwind", "Bootstrap"];
const backendTech = ["Node.js", "Express", "SQL", "Firebase"];
const tools = ["Postman", "VS Code", "Figma", "GitHub", "Netlify", "Railway"];

const skills = {
    frontend: frontendTech.map(getTech),
    backend: backendTech.map(getTech),
    tools: tools.map(getTech)
};

const macDots = [
    'bg-[#ff5f57]', // Red
    'bg-[#ffbd2e]', // Yellow
    'bg-[#28c840]'  // Green
];

const apexmotorLogo = "https://res.cloudinary.com/dexr27qho/image/upload/v1778567950/apexmotorlogo_fosrpb.png";
const venubookingLogo = "https://res.cloudinary.com/dexr27qho/image/upload/v1778568299/venubookinglogo_lw4qwo.png";
const portfolioLogo = "https://res.cloudinary.com/dexr27qho/image/upload/v1778859324/seo-preview_bk78k6.png";
const uniform = "https://res.cloudinary.com/dexr27qho/image/upload/v1778568199/uniform_way5oy.jpg";

const projects = [
    {
        id: 1,
        title: "ApexMotor",
        description: "A comprehensive e-commerce platform for selling car parts, featuring full CRUD functionality and user authentication.",
        tech: ["React.js", "Express.js", "Node.js", "Firebase", "Tailwind CSS", "Cloudinary"],
        logo: apexmotorLogo,
        status: "Completed",
        gridStyle: "md:col-span-1 md:row-span-1 lg:col-span-2 lg:row-span-1" // Example grid spanning 2 columns on large screens
    },
    {
        id: 2,
        title: "VenuBooking",
        description: "A venue reservation platform designed to streamline event planning and booking processes.",
        tech: ["React.js", "Node.js", "SQL", "Tailwind CSS", "Cloudinary", "Stripe"],
        logo: venubookingLogo,
        status: "Completed",
        gridStyle: "md:col-span-1 md:row-span-1 lg:col-span-1 lg:row-span-2"
    },
    {
        id: 3,
        title: "Portfolio",
        description: "This very developer profile, designed as a creative CLI/IDE interface to showcase skills and projects.",
        tech: ["Vue.js", "Tailwind CSS", "Express.js", "Node.js", "Netlify"],
        logo: portfolioLogo,
        status: "Completed",
        gridStyle: "md:col-span-1 md:row-span-1 lg:col-span-1 lg:row-span-2"
    },
];

const educationData = [
    {
        title: "Royal University of Phnom Penh (RUPP)",
        subtitle: "Bachelor of Information Technology Engineering",
        date: "2023 - 2027",
        details: null,
    },
    {
        title: "Independent Development",
        subtitle: "Self-taught Full Stack Development",
        date: "2023 - Present",
        details: "Built and deployed 3+ full-stack projects using modern technologies",
    },
    {
        title: "C/C++ Programming Certificate",
        subtitle: "Addbook Computer Center",
        date: "2024",
        details: null,
    },
];

const languages = new Map([
    ["English", "Fluent"],
    ["Khmer", "Native"]
]);

const languageArray = Array.from(languages, ([language, fluency]) => ({ language, fluency }));

// Data array used for rendering contact information
const contactData = [
    { icon: ['fas', 'phone'], text: '+855 888 093 342', color: 'text-sky-400' },
    { icon: ['fas', 'envelope'], text: 'vsal0882@gmail.com', color: 'text-sky-400' },
    { icon: ['fas', 'globe'], text: 'https://chunvisal.pro', color: 'text-sky-400' },
    { icon: ['fas', 'location-dot'], text: 'Phnom Penh, Cambodia', color: 'text-sky-400' },
    { icon: ['fab', 'github'], text: 'github.com/ChunVisal', color: 'text-white' },
    { icon: ['fab', 'linkedin'], text: 'LinkedIn', color: 'text-sky-400' },
];

const softSkills = [
    { icon: ['fas', 'lightbulb'], name: 'Problem Solving', color: 'text-yellow-400' },
    { icon: ['fas', 'brain'], name: 'Self-learning', color: 'text-green-400' },
    { icon: ['fas', 'handshake'], name: 'Collaboration', color: 'text-sky-400' },
    { icon: ['fas', 'clock'], name: 'Time Management', color: 'text-orange-400' },
    { icon: ['fas', 'briefcase'], name: 'Project Management', color: 'text-purple-400' },
    { icon: ['fas', 'users'], name: 'Teamwork', color: 'text-pink-400' }
];



</script>

<template>
    <div class="cv-root relative w-full max-w-[1300px] mx-auto p-13 px-3 md:px-5">
        <RouterLink to="/" class="text-white hover:text-gray-300 underline cursor-pointer">
            ← Back to Projects
        </RouterLink>
        <div class="tab-card mt-2 relative border border-[#1e2633] shadow-md rounded-xl">

            <header
                class="flex flex-row flex-wrap items-center justify-between px-3 py-3 sm:px-5 bg-[#1f2430] border-b border-[#2a3140] gap-2">
                <div class="flex items-center gap-2">
                    <div class="flex gap-2">
                        <span v-for="dot in macDots" :key="dot" class="w-2.5 h-2.5 rounded-full" :class="dot"></span>
                    </div>
                    <div class="flex items-center gap-2 ml-2 sm:ml-4">
                        <font-awesome-icon :icon="['fas', 'file-code']" class="text-purple-400 text-xs sm:text-sm" />
                        <span class="font-mono text-xs sm:text-sm text-[#96a0b5]">
                            Developer.tsx
                        </span>
                    </div>
                </div>
                <div class="flex items-center justify-between w-auto gap-3">
                    <div class="items-center gap-2">
                        <font-awesome-icon :icon="['fas', 'terminal']" class="text-purple-400 text-sm" />
                        <span class="font-mono text-sm text-[#96a0b5]">
                            Full Stack Developer
                        </span>
                    </div>
                    <a href="/public/ChunVisal_Resume.pdf" download>
                        <button
                            class="flex cursor-pointer items-center gap-2 bg-[#3b2b5f]/60 border border-[#6e5a9c]/40 px-3 py-1 rounded-lg transition hover:bg-[#4b3c73]/70">
                            <span class="font-mono text-xs sm:text-sm">
                                <span class="text-yellow-300">download</span>
                                <span class="text-purple-400">(</span>
                                <span class="text-green-300">'CV.pdf'</span>
                                <span class="text-purple-400">)</span>
                            </span>
                            <font-awesome-icon :icon="['fas', 'download']" class="text-purple-400 text-xs sm:text-sm" />
                        </button>
                    </a>
                </div>
            </header>

            <div class="p-4 sm:p-10 font-mono text-xs sm:text-sm text-[#96a0b5] leading-relaxed space-y-1">

                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">01</span>
                    <div>
                        <span class="text-purple-400">import</span>
                        <span> { </span>
                        <span class="text-yellow-300">Developer</span>
                        <span> } </span>
                        <span class="text-purple-400">from</span>
                        <span class="text-green-400">'cambodia/phnom-penh'</span><span>;</span>
                    </div>
                </div>

                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">02</span>
                    <div>
                        <span class="text-purple-400">import</span>
                        <span> { </span>
                        <span class="text-yellow-300">React</span><span class="text-white">, </span>
                        <span class="text-yellow-300">Node</span><span class="text-white">, </span>
                        <span class="text-yellow-300">SQL</span><span class="text-white">, </span>
                        <span class="text-yellow-300">Firebase</span>
                        <span> } </span>
                        <span class="text-purple-400">from</span>
                        <span class="text-green-400">'@skills'</span><span>;</span>
                    </div>
                </div>

                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">03</span>
                    <div class="text-[#6b7280] italic">/* ... other imports ... */</div>
                </div>

                <div class="flex gap-4"><span class="text-[#4b5563] select-none w-5 text-right">04</span>
                    <div></div>
                </div>

                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">05</span>
                    <div>
                        <span class="text-purple-300">export</span>
                        <span class="ml-2 text-purple-300">class</span>
                        <span class="ml-2 text-yellow-300">ChunVisal</span>
                        <span class="ml-2 text-purple-300">extends</span>
                        <span class="ml-2 text-sky-400">Developer</span>
                        <span class="ml-2 text-[#96a0b5]">{</span>
                    </div>
                </div>

                <div
                    class="flex flex-col lg:flex-row pl-5 sm:pl-9 pt-3 w-full justify-between items-start gap-4 lg:gap-0">

                    <div
                        class="flex flex-col items-center justify-center w-full lg:w-1/5 max-w-xs lg:max-w-auto mr-0 lg:mr-6">
                        <img :src="uniform" alt="Chun Visal Profile" @click="showPreview = true"
                            class="w-auto h-31 sm:w-full sm:h-auto rounded-sm border-2 border-pink-400/50 p-1 cursor-pointer transition transform hover:scale-[1.05]" />
                        <span
                            class="mt-2 text-[10px] text-[#6b7280] whitespace-nowrap">src/assets/project/profile.jpg</span>
                    </div>
                    <Teleport to="body">
                        <div v-if="showPreview"
                            class="fixed inset-0 z-[9999] flex items-center justify-center bg-black/80"
                            @click.self="closePreview">
                            <!-- Close button -->
                            <button @click="closePreview"
                                class="absolute top-6 right-6 text-white text-4xl font-bold hover:text-pink-400">
                                ✕
                            </button>

                            <!-- Image -->
                            <img :src="uniform" alt="Profile Preview"
                                class="max-w-[90vw] max-h-[90vh] rounded-lg shadow-2xl" />
                        </div>
                    </Teleport>

                    <div class="flex-1 w-full lg:w-auto order-first lg:order-0">
                        <div class="">
                            <div class="text-[#6b7280] italic">// Constructor - Developer Profile</div>
                            <div class="ml-0 text-xl sm:text-lg">
                                <span class="text-red-400 text-3xl sm:text-4xl font-bold">this</span><span
                                    class="text-white text-3xl sm:text-4xl font-bold">.</span><span
                                    class="text-pink-400 text-3xl sm:text-4xl font-bold">name</span>
                                <span class="text-white text-3xl sm:text-4xl font-bold"> = </span>
                            </div>
                            <span class="text-green-300 text-3xl sm:text-5xl font-bold">"CHUN VISAL"</span>
                            <div class="ml-0 text-sm sm:text-lg">
                                <span class="text-sm text-red-400">this</span><span class="text-white">.</span><span
                                    class="text-sm text-pink-400">role</span>
                                <span class="text-sm text-white"> = </span>
                                <span class="text-green-300">"Full Stack Developer"</span>
                            </div>
                        </div>

                        <div class="space-y-1 mt-4">
                            <div class="text-[#6b7280] italic">// @description</div>
                            <div class="text-[#96a0b5] border-l-2 border-purple-400/50 pl-4 py-2 text-xs sm:text-sm">
                                <span class="text-[#6b7280]">/* </span>Passionate **Full Stack Developer** with hands-on
                                experience in
                                <span class="text-yellow-300">React</span>,
                                <span class="text-yellow-300">Node.js</span>,
                                <span class="text-yellow-300">SQL</span>,
                                <span class="text-yellow-300">Firebase</span>, and
                                <span class="text-yellow-300">Tailwind</span>. Strong problem-solving skills with a
                                focus on building functional and visually appealing web applications.
                                <span class="text-[#6b7280]"> */</span>
                            </div>
                        </div>
                    </div>

                    <div
                        class="w-full lg:w-2/7 mt-4 lg:-mt-10 rounded-md bg-gray-900/70 border border-gray-700 py-2 px-4 sm:px-6 order-last lg:order-0">
                        <div class="text-white text-sm">
                            <span class="text-sky-400">const</span>
                            <span class="ml-1">contact</span>
                            <span class="text-white"> = {</span>
                        </div>
                        <div class="text-xs sm:text-sm ml-4 space-y-1 py-2">
                            <div v-for="item in contactData" :key="item.text" class="flex items-center gap-2">
                                <font-awesome-icon :icon="item.icon" :class="item.color" class="w-3" />
                                <span class="text-white/80 whitespace-nowrap">{{ item.text }}</span>
                            </div>
                        </div>
                        <div class="text-white text-sm">};</div>
                    </div>

                </div>
                <div class="flex gap-4"><span class="text-[#4b5563] select-none w-5 text-right">06</span>
                    <div></div>
                </div>


                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">07</span>
                    <div class="ml-6">
                        <span class="text-purple-300">getSkills</span>
                        <span class="text-white">(</span><span class="text-white">)</span>
                        <span class="text-purple-300"> {</span>
                    </div>
                </div>

                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">08</span>
                    <div class="ml-12">
                        <span class="text-purple-300">return</span>
                        <span class="text-white"> {</span>
                    </div>
                </div>
                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">09</span>
                    <div class="ml-8 sm:ml-16"> <span class="text-sky-400">frontend</span><span class="text-white">:
                            [</span>
                    </div>
                </div>

                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">10</span>
                    <div class="ml-12 sm:ml-20 flex flex-wrap gap-2 sm:gap-3">
                        <div v-for="skill in skills.frontend" :key="skill.name"
                            class="flex items-center gap-1 px-2 py-0.5 sm:px-3 sm:py-1 rounded-lg bg-[#3b2b5f]/40 border border-[#6e5a9c]/30 text-xs">
                            <img :src="skill.url" class="w-4 h-4" :alt="skill.name">
                            <span class="text-[#e5d8ff]">{{ skill.name }}</span>
                        </div>
                    </div>
                </div>
                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">11</span>
                    <div class="ml-8 sm:ml-16 text-white">],</div>
                </div>

                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">12</span>
                    <div class="ml-8 sm:ml-16">
                        <span class="text-sky-400">backend</span><span class="text-white">: [</span>
                    </div>
                </div>

                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">13</span>
                    <div class="ml-12 sm:ml-20 flex flex-wrap gap-2 sm:gap-3">
                        <div v-for="skill in skills.backend" :key="skill.name"
                            class="flex items-center gap-1 px-2 py-0.5 sm:px-3 sm:py-1 rounded-lg bg-[#3b2b5f]/40 border border-[#6e5a9c]/30 text-xs">
                            <img :src="skill.url" class="w-4 h-4" :alt="skill.name">
                            <span class="text-[#e5d8ff]">{{ skill.name }}</span>
                        </div>
                    </div>
                </div>
                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">14</span>
                    <div class="ml-8 sm:ml-16 text-white">],</div>
                </div>


                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">15</span>
                    <div class="ml-8 sm:ml-16">
                        <span class="text-sky-400">tools</span><span class="text-white">: [</span>
                    </div>
                </div>

                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">16</span>
                    <div class="ml-12 sm:ml-20 flex flex-wrap gap-2 sm:gap-3">
                        <div v-for="tool in skills.tools" :key="tool.name"
                            class="flex items-center gap-1 px-2 py-0.5 sm:px-3 sm:py-1 rounded-lg bg-[#3b2b5f]/40 border border-[#6e5a9c]/30 text-xs">
                            <img :src="tool.url" class="w-4 h-4" :alt="tool.name">
                            <span class="text-[#e5d8ff]">{{ tool.name }}</span>
                        </div>
                    </div>
                </div>
                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">17</span>
                    <div class="ml-8 sm:ml-16 text-white">],</div>
                </div>

                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">18</span>
                    <div class="ml-8 sm:ml-16">
                        <span class="text-sky-400">softSkills</span><span class="text-white">: [</span>
                    </div>
                </div>

                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">19</span>
                    <div class="ml-12 sm:ml-20 flex flex-wrap gap-2 sm:gap-3">
                        <div v-for="skill in softSkills" :key="skill.name"
                            class="flex items-center gap-1 px-2 py-0.5 sm:px-3 sm:py-1 rounded-lg bg-[#3b2b5f]/40 border border-[#6e5a9c]/30 text-xs">
                            <font-awesome-icon :icon="skill.icon" :class="skill.color" />
                            <span class="text-[#e5d8ff]">{{ skill.name }}</span>
                        </div>
                    </div>
                </div>
                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">20</span>
                    <div class="ml-8 sm:ml-16 text-white">],</div>
                </div>

                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">21</span>
                    <div class="ml-12 text-white">};</div>
                </div>
                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">22</span>
                    <div class="ml-6 text-white">}</div>
                </div>

                <div class="flex gap-4"><span class="text-[#4b5563] select-none w-5 text-right">23</span>
                    <div></div>
                </div>
                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">24</span>
                    <div class="ml-6">
                        <span class="text-purple-300">async</span>
                        <span class="ml-2 text-purple-300">getProjects</span>
                        <span class="text-white">(</span><span class="text-white">)</span>
                        <span class="text-purple-300"> {</span>
                    </div>
                </div>
                <div class="flex pl-5 sm:pl-9 pt-3 w-full">
                    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 sm:gap-6 w-full">

                        <router-link :to="`/project/${project.id}`" v-for="project in projects" :key="project.title"
                            class="project-card cursor-pointer relative bg-[#1f2430] rounded-xl border border-[#2a3140] shadow-xl transform transition duration-500 hover:scale-[1.01] hover:shadow-2xl col-span-1 overflow-visible">
                            <div
                                class="flex items-center justify-between px-3 py-2 sm:px-4 sm:py-3 bg-[#1f2430] border-b border-[#2a3140]">

                                <div class="flex items-center gap-2">
                                    <img :src="project.logo" :alt="`${project.title} Logo`"
                                        class="w-6 h-6 sm:w-8 sm:h-8" />
                                    <h3
                                        class="text-sm sm:text-lg font-bold text-sky-400 font-sans tracking-wide whitespace-wrap">
                                        {{ project.title }}</h3>
                                </div>

                                <span class="text-[10px] sm:text-xs font-mono px-2 py-0.5 sm:px-3 sm:py-1 rounded-full"
                                    :class="project.status === 'Completed' ? 'bg-green-600/30 text-green-300' : 'bg-yellow-600/30 text-yellow-300'">
                                    {{ project.status }}
                                </span>
                            </div>

                            <div class="p-3 sm:p-4 space-y-2 sm:space-y-3">
                                <p class="text-xs sm:text-sm mb-2 border-l-2 border-purple-400/50 pl-3 italic">
                                    <span class="text-[#6b7280]">/* </span class="">{{ project.description }}<span
                                        class="text-[#6b7280]"> */</span>
                                </p>

                                <div class="flex flex-wrap gap-1 sm:gap-2 pt-2 border-t border-[#4b5563]/50">
                                    <span v-for="tech in project.tech" :key="tech"
                                        class="text-[10px] sm:text-xs px-1.5 py-0.5 rounded-md bg-blue-600/30 text-gray-200 font-mono">
                                        {{ tech }}
                                    </span>
                                </div>
                            </div>
                        </router-link>

                    </div>
                </div>

                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">45</span>
                    <div class="ml-6 text-white">}</div>
                </div>

                <div class="flex gap-4"><span class="text-[#4b5563] select-none w-5 text-right">46</span>
                    <div></div>
                </div>

                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">47</span>
                    <div class="ml-6">
                        <span class="text-purple-300">getEducation</span>
                        <span class="text-white">(</span><span class="text-white">)</span>
                        <span class="text-purple-300"> {</span>
                    </div>
                </div>

                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">48</span>
                    <div class="ml-10 sm:ml-12"> <span class="text-purple-300">return</span>
                        <span class="text-white"> [</span>
                    </div>
                </div>

                <div v-for="(item, index) in educationData" :key="item.title" class="flex gap-4 items-start py-2">
                    <span class="text-[#4b5563] select-none w-5 text-right">{{ 49 + index }}</span>
                    <div class="ml-10 sm:ml-16 w-full relative group min-h-20">
                        <div class="absolute -left-5 sm:-left-10 top-0 h-full">
                            <div class="w-3 h-3 rounded-full bg-pink-500/80 shadow-md"></div>
                            <div v-if="index < educationData.length - 1"
                                class="absolute left-1/2 top-3 bottom-0 w-0.5 bg-pink-500/20 transform -translate-x-1/2">
                            </div>
                        </div>

                        <div class="space-y-1">
                            <div class="text-white text-sm sm:text-base font-semibold">{{ item.title }}</div>

                            <div class="text-sky-300 text-xs sm:text-sm font-light">{{ item.subtitle }}</div>

                            <span
                                class="text-xs font-mono px-2 py-0.5 rounded bg-green-600/30 text-green-300 mt-1 inline-block">
                                {{ item.date }}
                            </span>

                            <p v-if="item.details" class="text-xs sm:text-sm text-[#96a0b5] mt-1 mb-2">{{ item.details
                            }}</p>
                        </div>
                    </div>
                </div>
                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">{{ 49 + educationData.length }}</span>
                    <div class="ml-10 sm:ml-12 text-white">];</div>
                </div>

                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">{{ 50 + educationData.length }}</span>
                    <div class="ml-6 text-white">}</div>
                </div>

                <div class="flex gap-4"><span class="text-[#4b5563] select-none w-5 text-right">{{ 51 +
                    educationData.length }}</span>
                    <div></div>
                </div>

                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">{{ 52 + educationData.length }}</span>
                    <div class="ml-6">
                        <span class="text-purple-300">getLanguages</span>
                        <span class="text-white">(</span><span class="text-white">)</span>
                        <span class="text-purple-300"> {</span>
                    </div>
                </div>

                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">{{ 53 + educationData.length }}</span>
                    <div class="ml-10 sm:ml-12"> <span class="text-purple-300">return</span>
                        <span class="text-white"> [</span>
                    </div>
                </div>

                <div v-for="(lang, index) in languageArray" :key="lang.language" class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">{{ 54 + educationData.length + index
                    }}</span>
                    <div class="ml-10 sm:ml-16"> <span class="text-white">{ </span>
                        <span class="text-sky-400 text-xs sm:text-sm">language</span><span class="text-white">: </span>
                        <span class="text-green-300 text-xs sm:text-sm">"{{ lang.language }}"</span><span
                            class="text-white">, </span>
                        <span class="text-sky-400 text-xs sm:text-sm">fluency</span><span class="text-white">: </span>
                        <span class="text-green-300 text-xs sm:text-sm">"{{ lang.fluency }}"</span>
                        <span class="text-white"> }</span><span class="text-white">{{ index < languageArray.length - 1
                            ? ',' : '' }}</span>
                    </div>
                </div>
                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">{{ 54 + educationData.length +
                        languageArray.length }}</span>
                    <div class="ml-10 sm:ml-12 text-white">];</div>
                </div>
                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">{{ 55 + educationData.length +
                        languageArray.length }}</span>
                    <div class="ml-6 text-white">}</div>
                </div>

                <div class="flex gap-4"><span class="text-[#4b5563] select-none w-5 text-right">{{ 56 +
                    educationData.length + languageArray.length }}</span>
                    <div></div>
                </div>

                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">{{ 57 + educationData.length +
                        languageArray.length }}</span>
                    <div>
                        <span class="text-white">}</span>
                        <span class="text-[#6b7280]"> // End of class ChunVisal</span>
                    </div>
                </div>

                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">{{ 58 + educationData.length +
                        languageArray.length }}</span>
                    <div>
                        <span class="text-purple-300">export</span>
                        <span class="ml-2 text-purple-300">default</span>
                        <span class="ml-2 text-white">new</span>
                        <span class="ml-2 text-yellow-300">ChunVisal</span>
                        <span class="text-white">(</span><span class="text-white">)</span><span
                            class="text-white">;</span>
                    </div>
                </div>

                <div class="flex gap-4">
                    <span class="text-[#4b5563] select-none w-5 text-right">{{ 59 + educationData.length +
                        languageArray.length }}</span>
                    <div>
                        <span class="text-[#6b7280]">// Built with Vue & JavaScript • 2025</span>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
div {
    -webkit-font-smoothing: antialiased;
}

.cv-root {
    backdrop-filter: blur(1px);
}

.tab-card {
    background: rgba(15, 21, 36, 0.91);
}

.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}

.modal-overlay {
    position: fixed;
    inset: 0;
    background: rgba(0, 0, 0, 0.85);

    display: flex;
    align-items: center;
    justify-content: center;

    z-index: 999999;
}

.modal-image {
    max-width: 90vw;
    max-height: 90vh;
    border-radius: 12px;
}
</style>