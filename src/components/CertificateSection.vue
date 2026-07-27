<template>
    <section class="text-white mt-20" id="certificates">
        <div class="px-4 xl:pl-16">
            <h2 class="text-4xl font-bold text-white mb-4">{{ langs("title") }}</h2>
        </div>
        <ul
            class="px-4 xl:px-16 sm:py-16 grid grid-cols-1 gap-6 pt-10 sm:grid-cols-2 lg:grid-cols-3 md:gap-10 md:pt-12">
            <li v-for="(certificate, index) in certificates" :key="certificate.id" data-aos="fade-up"
                :data-aos-delay="index * 100"
                class="flex items-start rounded-xl p-5 bg-[#111a3e] shadow-lg border border-[#1f1641] transition hover:border-primary hover:scale-[1.02] duration-200">
                <div class="w-16 h-16 shrink-0 rounded-lg overflow-hidden bg-white flex items-center justify-center">
                    <img v-if="certificate.logo && !failedLogos[certificate.id]" :src="certificate.logo"
                        :alt="certificate.issuer" class="w-full h-full object-cover" loading="lazy"
                        @error="onLogoError(certificate.id)" />
                    <div v-else
                        class="w-full h-full flex items-center justify-center bg-gradient-to-br from-primary to-secondary">
                        <span class="text-white font-bold text-lg">{{
                            initials(certificate.issuer)
                        }}</span>
                    </div>
                </div>
                <div class="pl-4 flex-1 min-w-0">
                    <h3 class="text-lg font-semibold text-white leading-snug">
                        {{ langs(`certificates.${certificate.slug}.title`) }}
                    </h3>
                    <p class="text-[#ADB7BE] text-sm">{{ certificate.issuer }}</p>
                    <p class="text-[#ADB7BE] text-xs mt-1">
                        {{ langs("issued") }}
                        {{ langs(`certificates.${certificate.slug}.issueDate`) }}
                    </p>
                    <p v-if="certificate.id" class="text-[#ADB7BE] text-xs break-all">
                        {{ langs("credentialId") }} {{ certificate.id }}
                    </p>
                    <a v-if="certificate.credentialUrl" :href="certificate.credentialUrl" target="_blank"
                        rel="noopener noreferrer"
                        class="inline-block mt-3 text-xs font-semibold px-4 py-1.5 rounded-full border border-primary text-primary hover:bg-primary hover:text-white transition">
                        {{ langs("showCredential") }}
                    </a>
                </div>
            </li>
        </ul>
    </section>
</template>

<script setup lang="ts">
import { reactive, ref } from "vue";
import { useI18n } from "vue-i18n";

const langs = (key: string) => useI18n().t(`certificateSection.${key}`);

const logoBase = "/hansfolio/assets/icons";

const certificates = ref([
    {
        id: "f886ce0f-69f8-48ad-ae2f-de3e2498aaea",
        issuer: "Aestech",
        logo: `${logoBase}/companies/aestech.jpg`,
        credentialUrl:
            "https://cert.aestech.co.id/f886ce0f-69f8-48ad-ae2f-de3e2498aaea?sig=CsuIZTFUpbR2-QtYorISscv5fL0XpgPRB1MS51sO55c",
        slug: "engineeringAward",
    },
    {
        id: "7cebc2f7-1a70c0-dcf4-56-08ae66c0bb3f",
        issuer: "tixu.ai",
        logo: "",
        credentialUrl:
            "https://tixu.ai/certificate/7cebc2f7-1a70c0-dcf4-56-08ae66c0bb3f",
        slug: "claudeVibeCoding",
    },
    {
        id: "53cd0974-1a70c0-de5e-55-b398aa46cdbf",
        issuer: "tixu.ai",
        logo: "",
        credentialUrl:
            "https://tixu.ai/certificate/53cd0974-1a70c0-de5e-55-b398aa46cdbf",
        slug: "claudeAdvancedWorkflows",
    },
    {
        id: "5ce75fbc-1a70c0-fad3-50-c4a69d0a2645",
        issuer: "tixu.ai",
        logo: "",
        credentialUrl:
            "https://tixu.ai/certificate/5ce75fbc-1a70c0-fad3-50-c4a69d0a2645",
        slug: "claudeCertification",
    },
]);

const failedLogos = reactive<Record<string, boolean>>({});
const onLogoError = (id: string) => {
    failedLogos[id] = true;
};

const initials = (name: string): string => {
    if (!name) return "?";
    return name
        .trim()
        .split(/\s+/)
        .map((word) => word[0])
        .join("")
        .slice(0, 2)
        .toUpperCase();
};
</script>