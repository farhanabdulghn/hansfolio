<template>
  <div class="bg-[#111827] min-h-screen">
    <Suspense>
      <template #default>
        <div>
          <NavBar />
          <HeroSection />
          <ServiceSection />
          <AboutSection />
          <ExperienceAndSkillSection />
          <LatestProjectSection />
          <CertificateSection />
          <ContactSection />
          <FooterSection />
          <BackToTop />
        </div>
      </template>
      <template #fallback>
        <div class="flex justify-center items-center min-h-screen">
          <LoadingSpinner />
        </div>
      </template>
    </Suspense>
  </div>
</template>

<script setup>
import { defineAsyncComponent } from "vue";
import HeroSection from "./components/HeroSection.vue";
import ServiceSection from "./components/ServiceSection.vue";
import AboutSection from "./components/AboutSection.vue";
import ExperienceAndSkillSection from "./components/ExperienceAndSkillSection.vue";
import LatestProjectSection from "./components/LatestProjectSection.vue";
import CertificateSection from "./components/CertificateSection.vue";
import ContactSection from "./components/ContactSection.vue";
import FooterSection from "./components/FooterSection.vue";
import BackToTop from "./components/BackToTop.vue";
import LoadingSpinner from "./components/LoadingSpinner.vue";

const NavBar = defineAsyncComponent(() => import('@/components/NavBar.vue'));

</script>
<style>
* {
  scrollbar-width: thin;
  scrollbar-color: #111827 #f1f1f1;
}
</style>