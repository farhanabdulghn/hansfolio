<template>
    <footer class="mt-8 border z-10 border-t-[#33353F] border-l-transparent border-r-transparent text-white">
        <div class="container p-12 flex justify-between">
            <img src="/assets/icons/logo.png" alt="logo-hans" class="h-20 w-auto">
            <p class="text-slate-600">© {{ currentYear }} Farhan Abdul Ghani. All rights reserved.</p>
        </div>
    </footer>
</template>

<script setup lang="ts">
const currentYear = new Date().getFullYear();
</script>