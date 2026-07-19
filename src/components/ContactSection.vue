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
                            <img :src="`https://img.icons8.com/?size=50&id=${contact.id}&format=png&color=ffffff`"
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
    {
        id: '12623',
        title: 'Email',
        subtitle: myEmail,
        icon: 'email',
        onclick(): string {
            return buildGmailUrl({ to: this.subtitle });
        },
    },
    {
        id: '106562',
        title: 'Github',
        subtitle: 'farhanabdulghn',
        icon: 'github',
        onclick(): string {
            return `https://github.com/${this.subtitle}`;
        }
    },
    {
        id: '17950',
        title: 'Google Dev',
        subtitle: 'farhanabdulghn',
        icon: 'google-developers',
        onclick(): string {
            return `http://g.dev/${this.subtitle}`;
        }
    },
    {
        id: '16733',
        title: 'Whatsapp',
        subtitle: '+6285117115655',
        icon: 'whatsapp',
        onclick(): string {
            return `https://wa.me/${this.subtitle}`;
        }
    },
    {
        id: '8808',
        title: 'Linkedin',
        subtitle: 'farhanabdulghn',
        icon: 'linkedin',
        onclick(): string {
            return `https://www.linkedin.com/in/${this.subtitle}/`;
        },
    },
    {
        id: '32309',
        title: 'Instagram',
        subtitle: '@farhanabdulghn',
        icon: 'instagram-new',
        onclick(): string {
            return `https://www.instagram.com/${this.subtitle.substring(1)}`;
        },
    },
    {
        id: '118467',
        title: 'Facebook',
        subtitle: 'farhan.a.ghani.90',
        icon: 'facebook-new',
        onclick(): string {
            return `https://www.facebook.com/${this.subtitle}`;
        }
    },
    {
        id: 'phOKFKYpe00C',
        title: 'X',
        subtitle: 'Farhan180202',
        icon: 'twitterx',
        onclick(): string {
            return `https://x.com/${this.subtitle}`;
        }
    },
]);

const form = reactive<ContactForm>({
    email: '',
    subject: '',
    message: '',
});

const sendMessage = (): void => {
    const body = `Dari: ${form.email}\n\n${form.message}`;
    const url = buildGmailUrl({
        to: myEmail,
        subject: form.subject || `Pesan dari ${form.email}`,
        body,
    });

    window.open(url, '_blank', 'noopener,noreferrer');
};
</script>