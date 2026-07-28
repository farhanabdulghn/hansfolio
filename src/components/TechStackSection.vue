<template>
    <section class="text-white mt-20" id="currently-learning">
        <div class="px-4 xl:pl-16">
            <h2 class="text-4xl font-bold text-white mb-2">{{ langs("title") }}</h2>
            <p class="text-[#adb7be] mb-8 max-w-2xl">{{ langs("subtitle") }}</p>
        </div>
        <ul class="px-4 xl:px-16 grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-4 gap-4">
            <li v-for="(tech, index) in techs" :key="tech.slug" data-aos="fade-up" :data-aos-delay="index * 80"
                class="flex items-center gap-3 rounded-xl px-4 py-3 bg-[#111a3e] shadow-lg border border-[#1f1641] transition hover:border-primary hover:scale-[1.02] duration-200">
                <span class="w-2.5 h-2.5 rounded-full shrink-0 bg-gradient-to-br from-primary to-secondary"></span>
                <span class="text-sm font-medium text-white truncate">{{ tech.name }}</span>
            </li>
        </ul>
    </section>
</template>

<script setup lang="ts">
import { ref } from "vue";
import { useI18n } from "vue-i18n";

interface Tech {
    slug: string;
    name: string;
}

const langs = (key: string) => useI18n().t(`techStackSection.${key}`);

const techs = ref<Tech[]>([
    { slug: "typescript", name: "TypeScript" },
    { slug: "golang", name: "Golang" },
    { slug: "docker", name: "Docker" },
    { slug: "graphql", name: "GraphQL" },
    { slug: "githubActions", name: "CI/CD (GitHub Actions)" },
    { slug: "claudeCode", name: "Claude Code / AI-Assisted Dev" },
]);
</script>