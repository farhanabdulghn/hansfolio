<template>
    <section class="text-white mt-20" id="about">
        <div class="absolute z-0 top-[93rem] inset-x-0 h-64 flex items-start">
            <div class="h-24 w-64 bg-gradient-to-br from-primary via-secondary blur-2xl to-[#570cac] opacity-20"></div>
        </div>
        <div class="md:grid md:grid-cols-2 gap-8 items-center py-8 px-4 xl:gap-16 sm:py-16 xl:px-16 z-1">
            <div data-aos="flip-right">
                <h2 class="text-4xl font-bold text-white text-left mb-8">{{ langs("titleEdu") }}</h2>
                <div class="space-y-8 py-8">
                    <div v-for="(education, index) in educations" :key="education.school"
                        class="flex items-center md:w-[80%] w-full p-5 rounded-xl bg-[#111a3e] shadow-lg border border-[#1f1641]">
                        <div class="w-1/4">
                            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor"
                                class="w-14 h-14 text-white">
                                <path
                                    d="M12 2 1 7l11 5 9-4.09V17h2V7L12 2Zm0 7.18L4.24 6 12 3.82 19.76 6 12 9.18ZM5 13v3.5C5 18.98 8.13 21 12 21s7-2.02 7-4.5V13l-7 3.18L5 13Z" />
                            </svg>
                        </div>
                        <div class="w-3/4 pl-4">
                            <h3
                                class="text-2xl font-semibold uppercase text-transparent bg-clip-text bg-gradient-to-r from-primary to-secondary lg:text-xl">
                                {{ education.school }}
                            </h3>
                            <p class="text-white">{{ langs(`educations[${index}].title`) }}</p>
                            <p class="text-white">{{ langs(`educations[${index}].years`) }}</p>
                        </div>
                    </div>
                </div>
            </div>
            <div class="mt-4 md:mt-0 text-left flex flex-col z-10 h-full" data-aos="flip-right">
                <h2 class="text-4xl font-bold text-white md:text-center text-left mb-4">{{ langs("titleAbout[0]") }}
                    <span class="text-transparent bg-clip-text bg-gradient-to-r from-primary to-secondary">{{
                        langs("titleAbout[1]") }}</span>
                    {{ langs("titleAbout[2]") }}
                </h2>
                <p class="text-base lg:text-lg mt-8 py-8">
                    {{ $t('aboutSection.desc') }}
                </p>
                <div class="flex justify-center items-center pt-8">
                    <div ref="statsRef" class="grid grid-cols-3 gap-4 max-w-lg">
                        <div v-for="(stat, index) in stats" :key="stat.label"
                            class="text-center rounded-xl bg-[#111a3e] shadow-lg border border-[#1f1641] p-3">
                            <h3 class="text-white font-bold text-xl sm:text-2xl lg:text-3xl">
                                +{{ displayedValues[index] }}
                            </h3>
                            <p class="text-sm sm:text-base text-gray-300">{{ stat.label }}</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup lang="ts">
import { ref, computed, onMounted, onUnmounted } from 'vue';
import { useI18n } from 'vue-i18n';

interface Education { school: string; }
interface Stat { target: number; label: string; }

const langs = (key: string) => useI18n().t(`aboutSection.${key}`);

const startDate = new Date(2022, 8);

const yearsExperience = computed(() => {
    const now = new Date();
    let years = now.getFullYear() - startDate.getFullYear();

    const hasNotPassed =
        now.getMonth() < startDate.getMonth() ||
        (now.getMonth() === startDate.getMonth() &&
            now.getDate() < startDate.getDate());

    if (hasNotPassed) years--;

    return years;
});

const educations = ref<Education[]>([
    { school: 'Politeknik LP3I' },
])

const stats = ref<Stat[]>([
    { target: 5, label: 'Happy Client' },
    { target: 25, label: 'Projects' },
    { target: yearsExperience.value, label: 'Years Experience' },
]);

const displayedValues = ref<number[]>(stats.value.map(() => 0));
const hasAnimated = ref(false);
const statsRef = ref<HTMLElement | null>(null);
let statsObserver: IntersectionObserver | null = null;

const animateCountUp = () => {
    if (hasAnimated.value) return;
    hasAnimated.value = true;

    const duration = 1500;
    const startTime = performance.now();

    const step = (now: number) => {
        const progress = Math.min((now - startTime) / duration, 1);
        const eased = 1 - Math.pow(1 - progress, 3);

        displayedValues.value = stats.value.map((stat) =>
            Math.round(stat.target * eased)
        );

        if (progress < 1) {
            requestAnimationFrame(step);
        }
    };

    requestAnimationFrame(step);
};

onMounted(() => {
    if (!statsRef.value) return;

    statsObserver = new IntersectionObserver(
        (entries) => {
            entries.forEach((entry) => {
                if (entry.isIntersecting) {
                    animateCountUp();
                }
            });
        },
        { threshold: 0.3 }
    );

    statsObserver.observe(statsRef.value);
});

onUnmounted(() => {
    statsObserver?.disconnect();
});
</script>