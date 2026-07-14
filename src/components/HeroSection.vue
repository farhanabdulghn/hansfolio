`<template>
    <section class="relative w-full" data-aos="zoom-in-up">
        <div class="absolute top-0 inset-x-0 h-64 flex items-start">
            <div class="h-24 w-2/3 bg-gradient-to-br from-[#570cac] blur-2xl invisible opacity-40"></div>
            <div class="h-20 w-3/5 bg-gradient-to-e from-[#670ccf] opacity-40 blur-2xl"></div>
        </div>
        <div class="w-full px-5 sm:px-8 md:px-12 lg:px-8 max-w-screen-lg lg:max-w-screen-xl mx-auto relative">
            <div
                class="grid lg:grid-cols-2 gap-10 xl:gap-14 relative pt-24 lg:max-w-none max-w-2xl md:max-w-3xl mx-auto">
                <div class="lg:py-6">
                    <div class="text-center lg:text-left">
                        <h1 class="pt-4 text-white font-bold text-4xl md:text-5xl lg:text-6xl">
                            {{ langs("hi") }} <span
                                class="text-transparent bg-clip-text bg-gradient-to-r from-primary to-pink-500">
                                Farhan
                            </span>🤙🏻
                        </h1>
                    </div>
                    <p class="text-green-300 pt-8 text-center lg:text-left mx-auto max-w-xl">
                        {{ langs("desc") }}
                    </p>
                    <div class="flex items-center gap-3 pt-9 flex-col sm:flex-row sm:w-max sm:mx-auto lg:mx-0">
                        <button
                            class="px-6 md:px-7 py-3 rounded-full relative group w-full sm:w-max flex justify-center">
                            <span
                                class="absolute inset-0 rounded-3xl group-hover:scale-105 origin-center transition-all ease-in-out bg-primary border-2 border-transparent"></span>
                            <span class="relative flex items-center justify-center text-white">Hire Me</span>
                        </button>
                        <div class="relative" @mouseenter="showMenu = true" @mouseleave="showMenu = false">
                            <button
                                class="border border-primary px-6 md:px-7 py-3 rounded-full relative group w-full sm:w-max flex justify-center">
                                <div class="flex items-center">
                                    <svg class="download-icon" width="18" height="22" viewBox="0 0 18 22" fill="none"
                                        xmlns="http://www.w3.org/2000/svg">
                                        <path d="M13 9L9 13M9 13L5 9M9 13V1" stroke="#f59e0b" stroke-width="2"
                                            stroke-linecap="round" stroke-linejoin="round" />
                                        <path
                                            d="M1 17V18C1 18.7956 1.31607 19.5587 1.87868 20.1213C2.44129 20.6839 3.20435 21 4 21H14C14.7956 21 15.5587 20.6839 16.1213 20.1213C16.6839 19.5587 17 18.7956 17 18V17"
                                            stroke="#f59e0b" stroke-width="2" stroke-linecap="round" />
                                    </svg>
                                    <span class="pl-2 text-primary">Download Resume</span>
                                </div>
                            </button>
                            <transition enter-active-class="transition ease-out duration-150"
                                enter-from-class="opacity-0 -translate-y-1" enter-to-class="opacity-100 translate-y-0"
                                leave-active-class="transition ease-in duration-100"
                                leave-from-class="opacity-100 translate-y-0" leave-to-class="opacity-0 -translate-y-1">
                                <div v-if="showMenu"
                                    class="absolute top-12 left-0 w-max rounded-xl bg-[#111a3e] border border-[#1f1641] shadow-lg overflow-hidden z-50">
                                    <a href="/hansfolio/assets/resume.pdf" download="cv-FarhanAbdulGhani.pdf"
                                        class="block px-4 py-2.5 w-full text-left text-white text-sm transition hover:bg-[#1a1650]">
                                        Download CV
                                    </a>
                                    <button @click="downloadPortfolio"
                                        class="block px-4 py-2.5 w-full text-left text-white text-sm transition hover:bg-[#1a1650]">
                                        Download Portfolio
                                    </button>
                                </div>
                            </transition>
                        </div>
                    </div>
                </div>
                <div class="lg:h-full md:flex">
                    <div
                        class="flex w-full h-96 min-h-[24rem] lg:min-h-[none] lg:w-full lg:h-full items-center relative">
                        <div
                            class="absolute z-0 top-1/2 -translate-y-1/2 w-5/6 right-0 h-[calc(80%+20px)] bg-gradient-to-tr opacity-25 from-[#570cac] to-primary blur-2xl">
                        </div>
                        <div
                            class="absolute h-full z-10 p-2 -translate-y-1/2 top-1/2 lg:right-3 md:right-40 sm:right-16 rounded-full shadow-lg border border-primary">
                            <img src="/assets/images/top_picture.jpg" alt="Hero pic" width="500" height="auto"
                                loading="lazy" class="w-full h-full rounded-full object-cover">
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <div v-if="showModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 p-4">
        <div
            class="bg-white rounded-lg shadow-lg p-6 w-11/12 max-w-sm sm:max-w-md md:max-w-lg lg:max-w-xl overflow-y-auto">
            <h2 class="text-lg font-semibold mb-4 text-center">{{ langs("modal.title") }}</h2>
            <p class="text-gray-600 mb-6 text-center">{{ langs("modal.subtitle") }}</p>

            <div class="grid grid-cols-2 gap-2 sm:flex sm:flex-wrap sm:justify-center">
                <button v-for="(format, index) in fileFormats" :key="index" @click="downloadPortfolioFile(format)"
                    :class="getButtonClass(format)"
                    class="px-4 py-2 rounded text-white text-sm hover:bg-opacity-75 text-center">
                    Download {{ format.toUpperCase() }}
                </button>
            </div>

            <button @click="closeModal" class="mt-4 px-4 py-2 bg-gray-400 text-white rounded w-full hover:bg-gray-500">
                {{ langs("modal.cancel") }}
            </button>
        </div>
    </div>

</template>
<script setup>
import Aos from 'aos';
import 'aos/dist/aos.css';
import { ref } from 'vue';
import { useI18n } from 'vue-i18n';


const { locale } = useI18n();

Aos.init();

const showMenu = ref(false);
const showModal = ref(false);
const fileFormats = ['pdf', 'svg', 'pptx', 'jpg', 'png'];

const langs = (key) => useI18n().t(`heroSection.${key}`);

const downloadPortfolio = () => {
    showModal.value = true;
};



const downloadPortfolioFile = (format) => {
    const lang = locale.value === "id" ? "id" : "en";

    console.info(lang);
    let fileName;

    if (format === "pptx" || format === "pdf") {
        fileName = `hansfolio-${lang}.${format}`;
    } else if (["png", "svg", "jpg"].includes(format)) {
        fileName = `hansfolio-${lang}-${format}.zip`;
    } else {
        console.error("Unsupported format!");
        return;
    }

    const filePath = `/hansfolio/assets/portfolio/${lang}/${fileName}`;

    const link = document.createElement('a');
    link.href = filePath;
    link.download = fileName;
    link.click();

    closeModal();
};



const closeModal = () => {
    showModal.value = false;
};

const getButtonClass = (format) => {
    switch (format) {
        case 'pdf':
            return 'bg-red-500 hover:bg-red-600';
        case 'svg':
            return 'bg-green-500 hover:bg-green-600';
        case 'pptx':
            return 'bg-orange-500 hover:bg-orange-600';
        case 'jpg':
            return 'bg-yellow-500 hover:bg-yellow-600';
        case 'png':
            return 'bg-blue-500 hover:bg-blue-600';
        default:
            return 'bg-gray-400';
    }
};

</script>