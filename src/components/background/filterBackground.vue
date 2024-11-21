<script setup>
import { onMounted, ref } from 'vue';

const backgrounds = [
    "./images/noise-1.png",
    "./images/noise-3.png",
    "./images/noise-2.png",
    "./images/noise-4.png",
];

const currentBackground = ref(backgrounds[0]);

onMounted(() => {
    let index = 0;
    setInterval(() => {
        index = (index + 1) % backgrounds.length;
        currentBackground.value = backgrounds[index];
    },120);
});
</script>

<template>
    <div :style="{ backgroundImage: `url(${currentBackground})` }" class="filter absolute w-screen h-screen opacity-50 z-10"></div>
</template>