<template>
    <header class="flex justify-between items-center p-6 bg-opacity-50 relative z-20">
        <div>
            <img src="/assets/icons/logo.png" alt="logo-hans" class="h-20 w-auto">
        </div>
        <div class="md:hidden z-30">
            <button type="button" class="block focus:outline-none" @click="isMenuOpen = !isMenuOpen">
                <span v-if="isMenuOpen" class="text-5xl">
                    <img src="https://img.icons8.com/ios-filled/100/ffffff/delete-sign.png" alt="close" width="50"
                        height="50">
                </span>
                <span v-else class="text-5xl">
                    <img src="https://img.icons8.com/ios-filled/ffffff/menu--v6.png" alt="menu" width="50" height="50">
                </span>
            </button>
        </div>
        <nav :class="['fixed inset-0 z-20 flex flex-col items-center justify-center bg-[#111827] md:relative md:bg-transparent md:flex md:justify-between md:flex-row',
            isMenuOpen ? 'block' : 'hidden'
        ]">
            <ul class="flex flex-col items-center space-y-5 md:flex-row md:space-x-5 md:space-y-0">
                <li v-for="menu in menus" :key="menu.name">
                    <a :href="menu.href"
                        class="block text-white transition hover:text-primary ease-linear text-2xl md:text-lg"
                        @click="scrollToSection(menu.href)">
                        {{ langs(`${menu.name}`) }}
                    </a>
                </li>
                <li class="relative" v-click-outside="closeLangMenu">
                    <button type="button" @click="isLangOpen = !isLangOpen"
                        class="flex items-center gap-2 px-4 py-2 rounded-full bg-[#111a3e] border border-[#1f1641] text-white text-sm md:text-xs transition hover:border-primary">
                        <span class="text-base leading-none">{{ currentLanguage.flag }}</span>
                        <span class="uppercase tracking-wide">{{ currentLanguage.code }}</span>
                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor"
                            class="w-3.5 h-3.5 text-gray-300 transition-transform duration-200"
                            :class="{ 'rotate-180': isLangOpen }">
                            <path fill-rule="evenodd"
                                d="M5.23 7.21a.75.75 0 011.06.02L10 11.168l3.71-3.938a.75.75 0 111.08 1.04l-4.25 4.5a.75.75 0 01-1.08 0l-4.25-4.5a.75.75 0 01.02-1.06z"
                                clip-rule="evenodd" />
                        </svg>
                    </button>
                    <transition enter-active-class="transition ease-out duration-150"
                        enter-from-class="opacity-0 -translate-y-1" enter-to-class="opacity-100 translate-y-0"
                        leave-active-class="transition ease-in duration-100"
                        leave-from-class="opacity-100 translate-y-0" leave-to-class="opacity-0 -translate-y-1">
                        <ul v-if="isLangOpen"
                            class="absolute md:right-0 mt-2 min-w-[9rem] rounded-xl bg-[#111a3e] border border-[#1f1641] shadow-lg overflow-hidden z-30">
                            <li v-for="lang in languages" :key="lang.code">
                                <button type="button" @click="selectLocale(lang.code)"
                                    class="w-full flex items-center gap-3 px-4 py-2.5 text-sm text-left text-white transition hover:bg-[#1a1650]"
                                    :class="{ 'bg-gradient-to-r from-primary/20 to-secondary/20': currentLocale === lang.code }">
                                    <span class="text-base leading-none">{{ lang.flag }}</span>
                                    <span>{{ lang.name }}</span>
                                    <svg v-if="currentLocale === lang.code" xmlns="http://www.w3.org/2000/svg"
                                        viewBox="0 0 20 20" fill="currentColor" class="w-4 h-4 ml-auto text-primary">
                                        <path fill-rule="evenodd"
                                            d="M16.704 4.153a.75.75 0 01.143 1.052l-8 10.5a.75.75 0 01-1.127.075l-4.5-4.5a.75.75 0 011.06-1.06l3.894 3.893 7.48-9.817a.75.75 0 011.05-.143z"
                                            clip-rule="evenodd" />
                                    </svg>
                                </button>
                            </li>
                        </ul>
                    </transition>
                </li>
            </ul>
        </nav>
    </header>
</template>

<script setup>
import { ref, computed } from 'vue';
import { useI18n } from 'vue-i18n';

const langs = (key) => useI18n().t(`navBar.${key}`);

const menus = ref([
    { name: 'service', href: '#services' },
    { name: 'aboutMe', href: '#about' },
    { name: 'skills', href: '#skills' },
    { name: 'projects', href: '#projects' },
    { name: 'contact', href: '#contact' },
]);

const isMenuOpen = ref(false);
const scrollToSection = (href) => {
    isMenuOpen.value = false;
    const section = document.querySelector(href);
    if (section) {
        section.scrollIntoView({ behavior: 'smooth' })
    }
}

const { locale } = useI18n();

const languages = ref([
    { code: 'en', name: 'English', flag: '🇬🇧' },
    { code: 'id', name: 'Bahasa Indonesia', flag: '🇮🇩' },
]);

const currentLocale = computed({
    get: () => locale.value,
    set: (newLocale) => {
        locale.value = newLocale;
    },
});

const currentLanguage = computed(() =>
    languages.value.find((lang) => lang.code === currentLocale.value) || languages.value[0]
);

const isLangOpen = ref(false);

const selectLocale = (code) => {
    currentLocale.value = code;
    isLangOpen.value = false;
};

const closeLangMenu = () => {
    isLangOpen.value = false;
};

// Simple click-outside directive so the dropdown closes when clicking elsewhere
const vClickOutside = {
    mounted(el, binding) {
        el.__clickOutsideHandler__ = (event) => {
            if (!(el === event.target || el.contains(event.target))) {
                binding.value(event);
            }
        };
        document.addEventListener('click', el.__clickOutsideHandler__);
    },
    unmounted(el) {
        document.removeEventListener('click', el.__clickOutsideHandler__);
    },
};
</script>