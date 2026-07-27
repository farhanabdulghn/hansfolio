<template>
    <section class="text-white mt-20" id="services">
        <div class="px-4 xl:pl-16">
            <h2 class="text-4xl font-bold text-white mb-4">{{ langs("title") }}</h2>
        </div>
        <div
            class="py-8 xl:px-16 sm:py-16 grid grid-cols-1 gap-16 pt-10 sm:grid-cols-2 md:gap-10 md:pt-12 lg:grid-cols-2">
            <div v-for="service in services" :key="service.slug" data-aos="fade-up"
                class="px-8 py-12 rounded-xl bg-[#111a3e] shadow-lg border border-[#1f1641]">
                <div class="mx-auto h-24 w-24 text-center xl:h-28 xl:w-28 text-primary">
                    <svg v-if="service.icon === 'mobile'" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"
                        fill="none" stroke="currentColor" stroke-width="1.5" class="w-full h-full">
                        <rect x="7" y="2" width="10" height="20" rx="2" />
                        <line x1="11" y1="18" x2="13" y2="18" />
                    </svg>
                    <svg v-else xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                        stroke-width="1.5" class="w-full h-full">
                        <path d="M8 4 2 12l6 8M16 4l6 8-6 8" />
                    </svg>
                </div>
                <div class="text-center">
                    <h3
                        class="pt-8 text-lg font-semibold uppercase text-transparent bg-clip-text bg-gradient-to-r from-primary to-secondary lg:text-xl">
                        {{ service.name }}
                    </h3>
                    <p class="text-gray pt-4 text-sm group-hover:text-white md:text-base">
                        <span v-html="langs(`services.${service.slug}.description`)
                            .replace(
                                'Flutter',
                                '<span class=\'text-blue-500\'>Flutter</span>',
                            )
                            .replace(
                                'Vue.js',
                                '<span class=\'text-green-500\'>Vue.js</span>',
                            )
                            "></span>
                    </p>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup lang="ts">
import { ref } from "vue";
import { useI18n } from "vue-i18n";

interface Service {
    icon: "mobile" | "web";
    name: string;
    slug: string;
}

const langs = (key: string) => useI18n().t(`serviceSection.${key}`);

const services = ref<Service[]>([
    { icon: "mobile", name: "Mobile Developer", slug: "mobileDeveloper" },
    { icon: "web", name: "Web Development", slug: "webDevelopment" },
]);
</script>
