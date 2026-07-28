<template>
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
                                    <button @click="openResumePreview"
                                        class="block px-4 py-2.5 w-full text-left text-white text-sm transition hover:bg-[#1a1650]">
                                        Preview CV
                                    </button>
                                    <a :href="resumePath" :download="resume"
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

    <transition enter-active-class="transition ease-out duration-200" enter-from-class="opacity-0"
        enter-to-class="opacity-100" leave-active-class="transition ease-in duration-150" leave-from-class="opacity-100"
        leave-to-class="opacity-0">
        <div v-if="showModal" class="fixed inset-0 bg-black bg-opacity-60 flex items-center justify-center z-50 p-4">
            <transition enter-active-class="transition ease-out duration-200" enter-from-class="opacity-0 scale-95"
                enter-to-class="opacity-100 scale-100" leave-active-class="transition ease-in duration-150"
                leave-from-class="opacity-100 scale-100" leave-to-class="opacity-0 scale-95">
                <div v-if="showModal"
                    class="relative bg-[#111a3e] border border-[#1f1641] rounded-xl shadow-lg p-6 w-11/12 max-w-sm sm:max-w-md md:max-w-lg lg:max-w-xl overflow-y-auto">
                    <button @click="closeModal"
                        class="absolute top-4 right-4 text-[#adb7be] hover:text-white transition text-2xl leading-none">
                        &times;
                    </button>

                    <h2 class="text-lg font-semibold mb-2 text-center text-white">{{ langs("modal.title") }}</h2>
                    <p class="text-[#adb7be] text-sm mb-6 text-center">{{ langs("modal.subtitle") }}</p>

                    <div class="grid grid-cols-2 gap-3 sm:flex sm:flex-wrap sm:justify-center">
                        <button v-for="(format, index) in fileFormats" :key="index"
                            @click="downloadPortfolioFile(format)" :class="getButtonClass(format)"
                            class="px-4 py-3 rounded-xl bg-[#0d1330] border border-[#1f1641] text-sm font-semibold transition duration-200 hover:scale-[1.02] text-center">
                            Download {{ format.toUpperCase() }}
                        </button>
                    </div>
                    <button @click="closeModal"
                        class="mt-6 px-4 py-2.5 rounded-full border border-[#adb7be] text-white text-sm transition hover:border-white w-full">
                        {{ langs("modal.cancel") }}
                    </button>
                </div>
            </transition>
        </div>
    </transition>

    <transition enter-active-class="transition ease-out duration-200" enter-from-class="opacity-0"
        enter-to-class="opacity-100" leave-active-class="transition ease-in duration-150" leave-from-class="opacity-100"
        leave-to-class="opacity-0">
        <div v-if="showResumePreview"
            class="fixed inset-0 bg-black bg-opacity-60 flex items-center justify-center z-50 p-4">
            <transition enter-active-class="transition ease-out duration-200" enter-from-class="opacity-0 scale-95"
                enter-to-class="opacity-100 scale-100" leave-active-class="transition ease-in duration-150"
                leave-from-class="opacity-100 scale-100" leave-to-class="opacity-0 scale-95">
                <div v-if="showResumePreview"
                    class="relative bg-[#111a3e] border border-[#1f1641] rounded-xl shadow-lg p-4 sm:p-6 w-11/12 max-w-3xl">
                    <button @click="closeResumePreview"
                        class="absolute top-3 right-3 text-[#adb7be] hover:text-white transition text-2xl leading-none z-10">
                        &times;
                    </button>
                    <div class="flex items-center justify-center gap-3 mb-4">
                        <h2 class="text-lg font-semibold text-white">{{ langs("resumePreview.title") }}</h2>
                        <a :href="resumeFliplinkUrl" target="_blank" rel="noopener noreferrer"
                            :title="langs('resumePreview.openLinkTitle')"
                            class="flex items-center gap-1 text-xs font-semibold px-3 py-1.5 rounded-full border border-primary text-primary hover:bg-primary hover:text-white transition">
                            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none"
                                stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                                class="w-3.5 h-3.5">
                                <path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6" />
                                <path d="M15 3h6v6" />
                                <path d="M10 14 21 3" />
                            </svg>
                            {{ langs("resumePreview.openLink") }}
                        </a>
                    </div>
                    <div class="w-full rounded-lg overflow-hidden border border-[#1f1641]">
                        <iframe :src="resumeFliplinkUrl" width="100%" height="600" frameborder="0" allowfullscreen
                            class="block"></iframe>
                    </div>
                </div>
            </transition>
        </div>
    </transition>
</template>

<script setup lang="ts">
import Aos from 'aos';
import 'aos/dist/aos.css';
import { computed, ref } from 'vue';
import { useI18n } from 'vue-i18n';

type FileFormat = 'pdf' | 'svg' | 'pptx' | 'jpg' | 'png';
type LangCode = 'en' | 'id';

const { locale } = useI18n();

Aos.init();

const resume = ref<string>('Resume_Farhan_Abdul_Ghani.pdf');
const resumeFliplinkUrl = ref<string>('https://go.fliplink.me/view/5EB7ABCB-C8C6-4DF3-891F-31FF0888534D');
const showMenu = ref<boolean>(false);
const showModal = ref<boolean>(false);
const showResumePreview = ref<boolean>(false);
const fileFormats = ref<FileFormat[]>(['pdf', 'svg', 'pptx', 'jpg', 'png']);

const resumePath = computed<string>(() => `/hansfolio/assets/${resume.value}`);

const langs = (key: string): string => useI18n().t(`heroSection.${key}`);

const downloadPortfolio = (): void => {
    showModal.value = true;
};

const downloadPortfolioFile = (format: FileFormat): void => {
    const lang: LangCode = locale.value === 'id' ? 'id' : 'en';

    console.info(lang);
    let fileName: string;

    if (format === 'pptx' || format === 'pdf') {
        fileName = `hansfolio-${lang}.${format}`;
    } else if (['png', 'svg', 'jpg'].includes(format)) {
        fileName = `hansfolio-${lang}-${format}.zip`;
    } else {
        console.error('Unsupported format!');
        return;
    }

    const filePath = `/hansfolio/assets/portfolio/${lang}/${fileName}`;

    const link = document.createElement('a');
    link.href = filePath;
    link.download = fileName;
    link.click();

    closeModal();
};

const closeModal = (): void => {
    showModal.value = false;
};

const openResumePreview = (): void => {
    showMenu.value = false;
    showResumePreview.value = true;
};

const closeResumePreview = (): void => {
    showResumePreview.value = false;
};

const getButtonClass = (format: FileFormat): string => {
    switch (format) {
        case 'pdf':
            return 'text-red-400 hover:border-red-400';
        case 'svg':
            return 'text-green-400 hover:border-green-400';
        case 'pptx':
            return 'text-orange-400 hover:border-orange-400';
        case 'jpg':
            return 'text-yellow-400 hover:border-yellow-400';
        case 'png':
            return 'text-blue-400 hover:border-blue-400';
        default:
            return 'text-gray-400 hover:border-gray-400';
    }
};
</script>