<template>
    <section class="text-white mt-18" id="skills">
        <div class="relative right-0 top-[110rem] h-full w-full justify-end">
            <span class="flex opacity-20">
                <span class="w-16 h-32 rounded-1-full flex bg-primary blur-2xl"></span>
                <span class="w-16 h-32 rounded-1-full flex bg-[#f88fc2] blur-2xl mt-14"></span>
            </span>
        </div>
        <div class="md:grid md:grid-cols-2 gap-8 items-center py-8 px-4 xl:gap-16 xl:px-16">
            <div class="mt-4 md:mt-0 text-left flex flex-col z-10 h-full w-[80%]">
                <h2 class="text-4xl font-bold text-white text-left mb-4">{{ langs("titleSkill[0]") }}
                    <span class="text-transparent bg-clip-text bg-gradient-to-r from-primary to-secondary">{{
                        langs("titleSkill[1]") }}</span>
                </h2>
                <div class="mt-8" v-for="skill in skills" :key="skill.name">
                    <div class="flex items-end justify-between" data-aos="fade-right">
                        <h4 class="font-semibold uppercase text-white">
                            {{ skill.name }}
                        </h4>
                        <h3 class="text-2xl font-bold text-white">{{ skill.width }}</h3>
                    </div>
                    <div class="mt-2 h-1 w-full bg-[#131d30] rounded-full">
                        <div class="h-1 rounded-full bg-primary" :style="`width :${skill.width}`"></div>
                    </div>
                </div>
            </div>
            <div data-aos="flip-left">
                <h2 class="text-4xl font-bold text-white text-left mb-8 md:text-center md:mt-0 mt-8">{{
                    langs("titleExperience") }}</h2>
                <div class="space-y-8 py-8" data-aos="fade-left">
                    <div v-for="experience in experiences" :key="experience.company"
                        class="flex items-center rounded-xl p-4 bg-[#111a3e] shadow-lg border border-[#1f1641]">
                        <div class="w-1/4">
                            <img src="https://img.icons8.com/ios-filled/100/ffffff/lawyer.png" alt="lawyer">
                        </div>
                        <div class="w-3/4 pl-4">
                            <h3
                                class="text-2xl font-semibold uppercase text-transparent bg-clip-text bg-gradient-to-r from-primary to-secondary">
                                {{ experience.role }}
                            </h3>
                            <p class="text-white">{{ experience.company }}</p>
                            <p class="text-white">{{ langs(experience.date) }}</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
import { ref } from 'vue';
import { useI18n } from 'vue-i18n';

const langs = (key) => useI18n().t(`experienceAndSkillSection.${key}`);

const skills = ref([
    {
        name: 'Dart',
        width: '96%'
    },
    {
        name: 'HTML & CSS',
        width: '85%'
    },
    {
        name: 'JavaScript',
        width: '70%'
    },
    {
        name: 'PHP',
        width: '60%'
    },
]);

const experiences = ref([
    {
        role: 'Intern Full-stack Developer',
        company: 'PT. Bejana Investidata Globalindo',
        date: 'period[0]'
    },
    {
        role: 'Mobile Developer',
        company: 'PT. Ruang Konsul Indonesia',
        date: 'period[1]'
    },
    {
        role: 'Mobile Developer',
        company: 'PT. Aesthetic Teknologi Indonesia',
        date: 'period[2]'
    }
]);
</script>
