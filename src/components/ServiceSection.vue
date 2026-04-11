<template>
    <section class="text-white mt-20" id="services">
        <div class="px-4 xl:pl-16">
            <h2 class="text-4xl font-bold text-white mb-4">{{ langs('title') }}</h2>
        </div>
        <div
            class="py-8 xl:px-16 sm:py-16 grid grid-cols-1 gap-16 pt-10 sm:grid-cols-2 md:gap-10 md:pt-12 lg:grid-cols-2">
            <div v-for="service in services" :key="service.id" data-aos="fade-up"
                class="px-8 py-12 rounded-xl bg-[#111a3e] shadow-lg border border-[#1f1641]">
                <div class="mx-auto h-24 w-24 text-center xl:h-28 xl:w-28">
                    <div>
                        <img :src="service.icon" alt="service icon">
                    </div>
                </div>
                <div class="text-center">
                    <h3
                        class="pt-8 text-lg font-semibold uppercase text-transparent bg-clip-text bg-gradient-to-r from-primary to-secondary lg:text-xl">
                        {{ service.name }}
                    </h3>
                    <p class="text-gray pt-4 text-sm group-hover:text-white md:text-base">
                        <span
                            v-html="langs(service.description).replace('Flutter', '<span class=\'text-blue-500\'>Flutter</span>').replace('Vue.js', '<span class=\'text-green-500\'>Vue.js</span>')"></span>
                    </p>

                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
import { ref } from 'vue';
import { useI18n } from 'vue-i18n';

const langs = (key) => useI18n().t(`serviceSection.${key}`);

const services = ref([
    {
        id: 1,
        icon: 'https://img.icons8.com/?size=100&id=qTi7dvhQWqxW&format=png&color=ffffff',
        name: 'Mobile Developer',
        description: 'list[0].description'
    },
    {
        id: 2,
        icon: 'https://img.icons8.com/ios-filled/100/ffffff/google-code.png',
        name: 'Web Development',
        description: 'list[1].description'
    },
]);
</script>