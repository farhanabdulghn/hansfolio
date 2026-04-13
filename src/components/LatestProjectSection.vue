<template>
  <section class="text-white mt-20" id="projects">
    <div class="px-4 xl:pl-16">
      <div class="mb-4 md:flex md:justify-between xl:pr-16">
        <h2 class="text-4xl font-bold text-white">My Latest Projects</h2>
        <div class="flex space-x-4 mb-4 mt-5 md:mt-0">
          <button
            :class="{
              'text-primary': selectedCategory === category,
              'text-white': selectedCategory !== category,
            }"
            class="hover:text-primary"
            v-for="category in ['all', 'Web Development', 'Mobile App']"
            :key="category"
            @click="selectedCategory = category"
          >
            {{ category }}
          </button>
        </div>
      </div>
      <ul
        class="px-4 sm:py-16 xl:pr-16 grid grid-cols-1 gap-6 pt-10 sm:grid-cols-2 md:gap-10 md:pt-12 lg:grid-cols-3"
        data-aos="fade-right"
      >
        <div v-for="(project, index) in filteredProjects" :key="index">
          <div
            class="h-52 md:h-[24rem] rounded-t-xl relative group"
            :style="{
              backgroundImage: 'url(' + project.image + ')',
              backgroundSize: 'cover',
              backgroundPosition: 'center',
              backgroundRepeat: 'no-repeat',
            }"
          >
            <div
              class="overlay items-center justify-center absolute top-0 left-0 w-full h-full bg-[#181818] bg-opacity-0 hidden group-hover:flex group-hover:bg-opacity-80 transition-all duration-500"
            >
              <a
                class="h-14 w-14 mr-2 border-2 relative rounded-full border-[#ADB7BE] hover:border-white group/link"
                :href="project.webURL"
                target="_blank"
                rel="noopener noreferrer"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  fill="none"
                  viewBox="0 0 24 24"
                  stroke-width="1.5"
                  stroke="currentColor"
                  aria-hidden="true"
                  data-slot="icon"
                  class="h-10 w-10 text-[#ADB7BE] absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 cursor-pointer group-hover/link:text-white"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    d="M17.25 6.75 22.5 12l-5.25 5.25m-10.5 0L1.5 12l5.25-5.25m7.5-3-4.5 16.5"
                  ></path>
                </svg>
              </a>
              <button
                class="h-14 w-14 border-2 relative rounded-full border-[#ADB7BE] hover:border-white group/link"
                @click.stop="openPreview(project)"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  fill="none"
                  viewBox="0 0 24 24"
                  stroke-width="1.5"
                  stroke="currentColor"
                  aria-hidden="true"
                  data-slot="icon"
                  class="h-10 w-10 text-[#ADB7BE] absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 cursor-pointer group-hover/link:text-white"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    d="M2.036 12.322a1.012 1.012 0 0 1 0-.639C3.423 7.51 7.36 4.5 12 4.5c4.638 0 8.573 3.007 9.963 7.178.07.207.07.431 0 .639C20.577 16.49 16.64 19.5 12 19.5c-4.638 0-8.573-3.007-9.963-7.178Z"
                  ></path>
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    d="M15 12a3 3 0 1 1-6 0 3 3 0 0 1 6 0Z"
                  ></path>
                </svg>
              </button>
            </div>
          </div>
          <div
            class="text-white rounded-b-xl mt-3 bg-[#111a3e] shadow-lg border border-[#1f1641] py-6 px-4"
          >
            <h3 class="text-lg font-semibold lg:text-xl">
              {{ project.title }}
            </h3>
            <p class="text-[#ADB7BE]">{{ langs(`projects.desc[${index}]`) }}</p>
            <div class="flex flex-wrap p-2.5">
              <div
                v-for="technology in project.technologies"
                :key="technology.id"
                class="text-center ml-1 mt-1 rounded-3xl bg-[#111827]"
                style="
                  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
                  border: 1px solid #111827;
                  backdrop-filter: blur(9px);
                  -webkit-backdrop-filter: blur(9px);
                "
              >
                <p class="px-1 py-2">{{ technology }}</p>
              </div>
            </div>
          </div>
        </div>
      </ul>
    </div>
    <Teleport to="body">
      <div
        v-if="previewProject"
        class="fixed inset-0 z-50 flex items-center justify-center bg-black bg-opacity-80"
        @click.self="closePreview"
      >
        <div class="relative max-w-3xl w-full mx-4">
          <button
            class="absolute -top-10 right-0 text-white text-3xl hover:text-gray-300"
            @click="closePreview"
          >
            &times;
          </button>
          <div
            class="overflow-hidden max-h-[70vh] flex items-center justify-center rounded-xl select-none"
            :class="
              isDragging
                ? 'cursor-grabbing'
                : zoomLevel > 1
                  ? 'cursor-grab'
                  : 'cursor-default'
            "
            @wheel.prevent="onWheel"
            @mousedown="onMouseDown"
            @mousemove="onMouseMove"
            @mouseup="onMouseUp"
            @mouseleave="onMouseUp"
          >
            <img
              :src="previewProject.image"
              :alt="previewProject.title"
              :style="{
                transform: `scale(${zoomLevel}) translate(${translateX / zoomLevel}px, ${translateY / zoomLevel}px)`,
                transition: isDragging ? 'none' : 'transform 0.2s ease',
              }"
              class="rounded-xl object-contain max-h-[70vh] origin-center pointer-events-none"
              draggable="false"
            />
          </div>
          <p class="text-white text-center mt-3 text-lg font-semibold">
            {{ previewProject.title }}
          </p>
          <div class="flex items-center justify-center gap-3 mt-3">
            <button
              @click="zoomOut"
              :disabled="zoomLevel <= 0.5"
              class="h-9 w-9 flex items-center justify-center rounded-full border-2 border-[#ADB7BE] hover:border-white text-white disabled:opacity-30 disabled:cursor-not-allowed text-xl font-bold"
            >
              −
            </button>
            <button
              @click="zoomReset"
              class="px-3 py-1 rounded-full border-2 border-[#ADB7BE] hover:border-white text-white text-sm"
            >
              {{ Math.round(zoomLevel * 100) }}%
            </button>
            <button
              @click="zoomIn"
              :disabled="zoomLevel >= 3"
              class="h-9 w-9 flex items-center justify-center rounded-full border-2 border-[#ADB7BE] hover:border-white text-white disabled:opacity-30 disabled:cursor-not-allowed text-xl font-bold"
            >
              +
            </button>
            <button
              @click="zoomReset"
              :disabled="
                zoomLevel === 1 && translateX === 0 && translateY === 0
              "
              class="px-3 py-1 rounded-full border-2 border-[#ADB7BE] hover:border-white text-white text-sm disabled:opacity-30 disabled:cursor-not-allowed"
            >
              Reset
            </button>
          </div>
        </div>
      </div>
    </Teleport>
  </section>
</template>

<script setup>
import { computed, ref } from "vue";
import { useI18n } from "vue-i18n";

const langs = (key) => useI18n().t(`latestProjectSection.${key}`);
const previewProject = ref(null);
const zoomLevel = ref(1);
const translateX = ref(0);
const translateY = ref(0);
const isDragging = ref(false);
const dragStart = ref({ x: 0, y: 0 });

const openPreview = (project) => {
  previewProject.value = project;
  zoomLevel.value = 1;
  translateX.value = 0;
  translateY.value = 0;
};

const closePreview = () => {
  previewProject.value = null;
  zoomLevel.value = 1;
  translateX.value = 0;
  translateY.value = 0;
};

const zoomIn = () => {
  if (zoomLevel.value < 3)
    zoomLevel.value = +(zoomLevel.value + 0.25).toFixed(2);
};

const zoomOut = () => {
  if (zoomLevel.value > 0.5)
    zoomLevel.value = +(zoomLevel.value - 0.25).toFixed(2);
};

const zoomReset = () => {
  zoomLevel.value = 1;
  translateX.value = 0;
  translateY.value = 0;
};

const onWheel = (e) => {
  e.preventDefault();

  if (e.ctrlKey) {
    const delta = e.deltaY > 0 ? -0.15 : 0.15;
    const next = +(zoomLevel.value + delta).toFixed(2);
    zoomLevel.value = Math.min(3, Math.max(0.5, next));
  } else if (zoomLevel.value > 1) {
    translateX.value -= e.deltaX;
    translateY.value -= e.deltaY;
  }
};

const onMouseDown = (e) => {
  if (zoomLevel.value <= 1) return;
  isDragging.value = true;
  dragStart.value = {
    x: e.clientX - translateX.value,
    y: e.clientY - translateY.value,
  };
};

const onMouseMove = (e) => {
  if (!isDragging.value) return;
  translateX.value = e.clientX - dragStart.value.x;
  translateY.value = e.clientY - dragStart.value.y;
};

const onMouseUp = () => {
  isDragging.value = false;
};

const projects = ref(
  [
    {
      category: "Mobile App",
      image: "/hansfolio/assets/images/projects/quran_al_barkah.svg",
      title: "Quran Al Barkah",
      technologies: ["Flutter", "Android"],
      webURL:
        "https://play.google.com/store/apps/details?id=com.gridiyansapps.quran_al_barkah&pcampaignid=web_share",
    },
    {
      category: "Mobile App",
      image: "/hansfolio/assets/images/projects/aesline.webp",
      title: "AESLINE DISPLAY",
      technologies: ["Flutter", "Android TV", "Google TV"],
      webURL:
        "https://play.google.com/store/apps/details?id=io.aestech.aesline&pcampaignid=web_share",
    },
    {
      category: "Mobile App",
      image: "/hansfolio/assets/images/projects/qr_guest_book.webp",
      title: "QR Guest Book",
      technologies: ["Flutter", "Android"],
      webURL: "",
    },
    {
      category: "Mobile App",
      image: "/hansfolio/assets/images/projects/benings_app.webp",
      title: "Benings App",
      technologies: ["Flutter", "Android", "IOS"],
      webURL: "",
    },
    {
      category: "Mobile App",
      image: "/hansfolio/assets/images/projects/aestech.webp",
      title: "Aestech Customer (Unofficial Name)",
      technologies: ["Flutter", "Android", "IOS"],
      webURL: "",
    },
  ].map((item, index) => ({
    ...item,
    order: index,
  })),
);

const selectedCategory = ref("all");
const filteredProjects = computed(() => {
  if (selectedCategory.value === "all") {
    return projects.value;
  }
  return projects.value.filter(
    (project) =>
      project.category.toLowerCase() === selectedCategory.value.toLowerCase(),
  );
});
</script>
