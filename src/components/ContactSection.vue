<template>
    <section class="text-white mt-20" id="contact">
        <h2 class="text-4xl font-bold text-white text-left mb-4 px-4 xl:pl-16">{{ langs("title") }}</h2>
        <div class="grid md:grid-cols-2 gap-4 relative px-4 xl:px-16 mt-8 items-center" data-aos="zoom-in-up">
            <div>
                <p class="text-[#adb7be]">
                    {{ langs("desc") }}
                </p>
                <div v-for="contact in contacts" :key="contact.id" class="col-lg-4 col-mb-4 mb-lg-0 mt-5 mr-8">
                    <a :href="contact.onclick()" target="_blank" rel="noopener noreferrer"
                        class="flex mb-10 items-center transition transform hover:scale-105 hover:shadow-lg hover:bg-[#162043] rounded-lg p-4">
                        <div class="p-2 transition transform hover:scale-110"
                            style="background: #111a3e; width: 50px; height: 44px; display: flex; justify-content: center; border-radius: 50%; overflow: hidden; border: 1px solid #111a3e; backdrop-filter: blur(9px); -webkit-backdrop-filter: blur(9px);">
                            <img :src="`https://img.icons8.com/?size=50&id=${contact.idIcon}&format=png&color=ffffff`"
                                :alt="`${contact.icon}`" class="w-6">
                        </div>
                        <div class="ml-5 text-white">
                            <h4>{{ contact.title }}</h4>
                            <p>{{ contact.subtitle }}</p>
                        </div>
                    </a>
                </div>
            </div>
            <div
                style="background: #111a3e; width: 100%; height: 400px; border-radius: 20px; overflow: hidden; border: 1px solid#111a3e; backdrop-filter: blur(9px); -webkit-backdrop-filter: blur(9px);">
                <form class="flex flex-col p-4" data-aos="zoom-in-up">
                    <div class="mb-6">
                        <label for="email" class="text-white block mb-2 text-sm font-medium">email</label>
                        <input type="email" id="email"
                            class="bg-[#111827] placeholder:[#9CA2A9] text-gray-100 text-sm rounded-lg block w-full p-2.5"
                            placeholder="email@gmail.com" name="email">
                    </div>
                    <div class="mb-6">
                        <label for="subject" class="text-white block mb-2 text-sm font-medium">Subject</label>
                        <input type="subject" id="subject"
                            class="bg-[#111827] placeholder:[#9CA2A9] text-gray-100 text-sm rounded-lg block w-full p-2.5"
                            placeholder="subject" name="subject">
                    </div>
                    <div class="mb-6">
                        <label for="message" class="text-white block mb-2 text-sm font-medium">Message</label>
                        <textarea id="Message"
                            class="bg-[#111827] placeholder:[#9CA2A9] text-gray-100 text-sm rounded-lg block w-full p-2.5"
                            placeholder="Let's talk about..." name="Message"></textarea>
                    </div>
                    <button
                        class="z-1 w-[100%!important] px-6 md:px-7 py-3 rounded-full sm:w-max flex justify-center text-white bg-primary border-2 border-transparent">
                        Send Message
                    </button>
                </form>
            </div>
            <div
                class="bg-gradient-to-tr opacity-25 from-[#570cac] to-primary blur-2xl h-20 w-80 z-0 absolute -top-1/2 -left-4 transform -translate-x-2/3 -translate-1/2">
            </div>
        </div>
    </section>
</template>

<script setup>
import { ref } from 'vue';
import { useI18n } from 'vue-i18n';

const langs = (key) => useI18n().t(`contactSection.${key}`);

const contacts = ref([
    {
        id: 1,
        title: 'Email',
        subtitle: 'abgfarhan18@gmail.com',
        idIcon: '12623',
        onclick() {
            return `mailto:${this.subtitle}`;
        },
    },
    {
        id: 2,
        title: 'Linkedin',
        subtitle: 'www.linkedin.com',
        idIcon: '8808',
        onclick() {
            return `https://${this.subtitle}/in/farhan-ab-g-74001a260/`;
        },
    },
    {
        id: 3,
        title: 'Instagram',
        subtitle: '@farhanabdulghn',
        idIcon: '32309',
        onclick() {
            return `https://www.instagram.com/${this.subtitle.substring(1)}`;
        },
    },
    {
        id: 4,
        title: 'Github',
        subtitle: 'farhanabdulghn',
        idIcon: '106562',
        onclick() {
            return `https://github.com/${this.subtitle}`;
        }
    }
]);
</script>