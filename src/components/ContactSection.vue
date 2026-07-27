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
                        <div class="p-2 transition transform hover:scale-110 text-white"
                            style="background: #111a3e; width: 50px; height: 44px; display: flex; justify-content: center; align-items:center; border-radius: 50%; overflow: hidden; border: 1px solid #111a3e; backdrop-filter: blur(9px); -webkit-backdrop-filter: blur(9px);">
                            <svg v-if="contact.icon === 'email'" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                                stroke-width="1.5" class="w-6 h-6">
                                <rect x="3" y="5" width="18" height="14" rx="2" />
                                <path d="m3 7 9 6 9-6" />
                            </svg>
                            <svg v-else-if="contact.icon === 'github'" viewBox="0 0 24 24" fill="currentColor"
                                class="w-6 h-6">
                                <path
                                    d="M12 2C6.48 2 2 6.48 2 12c0 4.42 2.87 8.17 6.84 9.5.5.09.68-.22.68-.48 0-.24-.01-.87-.01-1.7-2.78.6-3.37-1.34-3.37-1.34-.45-1.16-1.11-1.47-1.11-1.47-.91-.62.07-.6.07-.6 1 .07 1.53 1.03 1.53 1.03.89 1.53 2.34 1.09 2.91.83.09-.65.35-1.09.63-1.34-2.22-.25-4.56-1.11-4.56-4.94 0-1.09.39-1.99 1.03-2.69-.1-.25-.45-1.27.1-2.65 0 0 .84-.27 2.75 1.03A9.6 9.6 0 0 1 12 6.8c.85 0 1.7.11 2.5.33 1.9-1.3 2.75-1.03 2.75-1.03.55 1.38.2 2.4.1 2.65.64.7 1.03 1.6 1.03 2.69 0 3.84-2.34 4.68-4.57 4.93.36.31.68.92.68 1.85 0 1.34-.01 2.42-.01 2.75 0 .27.18.58.69.48A10.01 10.01 0 0 0 22 12c0-5.52-4.48-10-10-10Z" />
                            </svg>
                            <svg v-else-if="contact.icon === 'google-developers'" viewBox="0 0 24 24" fill="none"
                                stroke="currentColor" stroke-width="1.5" class="w-6 h-6">
                                <rect x="3" y="4" width="18" height="16" rx="2" />
                                <path d="m7 9 3 3-3 3M13 15h4" />
                            </svg>
                            <svg v-else-if="contact.icon === 'whatsapp'" viewBox="0 0 24 24" fill="currentColor"
                                class="w-6 h-6">
                                <path
                                    d="M12.04 2C6.58 2 2.13 6.45 2.13 11.91c0 1.75.46 3.45 1.32 4.95L2 22l5.28-1.38a9.9 9.9 0 0 0 4.76 1.21h.01c5.46 0 9.91-4.45 9.91-9.91C21.96 6.45 17.5 2 12.04 2Zm5.8 14.19c-.24.68-1.39 1.32-1.92 1.4-.49.08-1.11.11-1.79-.11a15.8 15.8 0 0 1-1.63-.6c-2.87-1.24-4.74-4.12-4.88-4.31-.14-.19-1.17-1.55-1.17-2.96 0-1.4.74-2.09.99-2.38.26-.28.56-.35.75-.35h.54c.17 0 .4-.02.62.48.24.53.81 1.93.88 2.07.07.14.12.31.02.5-.09.19-.14.31-.28.48-.14.17-.29.37-.42.5-.14.14-.28.29-.12.57.16.28.72 1.2 1.55 1.94 1.06.95 1.96 1.24 2.24 1.38.28.14.44.12.6-.07.17-.19.7-.82.89-1.1.19-.28.38-.23.63-.14.26.09 1.65.78 1.94.93.28.14.47.21.54.33.07.12.07.71-.17 1.39Z" />
                            </svg>
                            <svg v-else-if="contact.icon === 'linkedin'" viewBox="0 0 24 24" fill="currentColor"
                                class="w-6 h-6">
                                <path
                                    d="M4.98 3.5C4.98 4.88 3.9 6 2.5 6S0 4.88 0 3.5 1.12 1 2.5 1s2.48 1.12 2.48 2.5ZM.24 8.25h4.48V23H.24V8.25ZM8.13 8.25h4.29v2.01h.06c.6-1.1 2.06-2.26 4.24-2.26 4.53 0 5.37 2.87 5.37 6.61V23h-4.48v-6.7c0-1.6-.03-3.66-2.28-3.66-2.28 0-2.63 1.72-2.63 3.55V23H8.13V8.25Z" />
                            </svg>
                            <svg v-else-if="contact.icon === 'instagram-new'" viewBox="0 0 24 24" fill="none"
                                stroke="currentColor" stroke-width="1.5" class="w-6 h-6">
                                <rect x="3" y="3" width="18" height="18" rx="5" />
                                <circle cx="12" cy="12" r="4" />
                                <circle cx="17.5" cy="6.5" r="1" fill="currentColor" stroke="none" />
                            </svg>
                            <svg v-else-if="contact.icon === 'facebook-new'" viewBox="0 0 24 24" fill="currentColor"
                                class="w-6 h-6">
                                <path
                                    d="M22 12a10 10 0 1 0-11.56 9.88v-6.99H7.9V12h2.54V9.8c0-2.5 1.49-3.89 3.77-3.89 1.09 0 2.24.2 2.24.2v2.46h-1.26c-1.24 0-1.63.77-1.63 1.56V12h2.78l-.44 2.89h-2.34v6.99A10 10 0 0 0 22 12Z" />
                            </svg>
                            <svg v-else viewBox="0 0 24 24" fill="currentColor" class="w-6 h-6">
                                <path
                                    d="M18.24 2H21l-6.5 7.43L22 22h-6.24l-4.9-6.4L4.9 22H2.14l7-8-7.14-9.98H8.3l4.44 5.87L18.24 2Zm-1.1 18h1.7L7 3.9H5.18L17.14 20Z" />
                            </svg>
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
                <form class="flex flex-col p-4" data-aos="zoom-in-up" @submit.prevent="sendMessage">
                    <div class="mb-6">
                        <label for="email" class="text-white block mb-2 text-sm font-medium">email</label>
                        <input type="email" id="email" v-model="form.email"
                            class="bg-[#111827] placeholder:[#9CA2A9] text-gray-100 text-sm rounded-lg block w-full p-2.5"
                            placeholder="email@gmail.com" name="email" required>
                    </div>
                    <div class="mb-6">
                        <label for="subject" class="text-white block mb-2 text-sm font-medium">Subject</label>
                        <input type="text" id="subject" v-model="form.subject"
                            class="bg-[#111827] placeholder:[#9CA2A9] text-gray-100 text-sm rounded-lg block w-full p-2.5"
                            placeholder="subject" name="subject">
                    </div>
                    <div class="mb-6">
                        <label for="message" class="text-white block mb-2 text-sm font-medium">Message</label>
                        <textarea id="message" v-model="form.message"
                            class="bg-[#111827] placeholder:[#9CA2A9] text-gray-100 text-sm rounded-lg block w-full p-2.5"
                            placeholder="Let's talk about..." name="message" required></textarea>
                    </div>
                    <button type="submit"
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

<script setup lang="ts">
import { reactive, ref } from 'vue';
import { useI18n } from 'vue-i18n';

interface Contact {
    id: string;
    title: string;
    subtitle: string;
    icon: string;
    onclick(this: Contact): string;
}

interface GmailUrlParams {
    to: string;
    subject?: string;
    body?: string;
}

interface ContactForm {
    email: string;
    subject: string;
    message: string;
}

const langs = (key: string) => useI18n().t(`contactSection.${key}`);

const myEmail = 'abgfarhan18@gmail.com';
const gmailComposeBase = 'https://mail.google.com/mail/?view=cm&fs=1';

const buildGmailUrl = ({ to, subject = '', body = '' }: GmailUrlParams): string => {
    const params = new URLSearchParams({ to, su: subject, body });
    return `${gmailComposeBase}&${params.toString()}`;
};

const contacts = ref<Contact[]>([
    { id: '12623', title: 'Email', subtitle: myEmail, icon: 'email', onclick(): string { return buildGmailUrl({ to: this.subtitle }); } },
    { id: '106562', title: 'Github', subtitle: 'farhanabdulghn', icon: 'github', onclick(): string { return `https://github.com/${this.subtitle}`; } },
    { id: '17950', title: 'Google Dev', subtitle: 'farhanabdulghn', icon: 'google-developers', onclick(): string { return `http://g.dev/${this.subtitle}`; } },
    { id: '16733', title: 'Whatsapp', subtitle: '+6285117115655', icon: 'whatsapp', onclick(): string { return `https://wa.me/${this.subtitle}`; } },
    { id: '8808', title: 'Linkedin', subtitle: 'farhanabdulghn', icon: 'linkedin', onclick(): string { return `https://www.linkedin.com/in/${this.subtitle}/`; } },
    { id: '32309', title: 'Instagram', subtitle: '@farhanabdulghn', icon: 'instagram-new', onclick(): string { return `https://www.instagram.com/${this.subtitle.substring(1)}`; } },
    { id: '118467', title: 'Facebook', subtitle: 'farhan.a.ghani.90', icon: 'facebook-new', onclick(): string { return `https://www.facebook.com/${this.subtitle}`; } },
    { id: 'phOKFKYpe00C', title: 'X', subtitle: 'Farhan180202', icon: 'twitterx', onclick(): string { return `https://x.com/${this.subtitle}`; } },
]);

const form = reactive<ContactForm>({ email: '', subject: '', message: '' });

const sendMessage = (): void => {
    const body = `Dari: ${form.email}\n\n${form.message}`;
    const url = buildGmailUrl({ to: myEmail, subject: form.subject || `Pesan dari ${form.email}`, body });
    window.open(url, '_blank', 'noopener,noreferrer');
};
</script>