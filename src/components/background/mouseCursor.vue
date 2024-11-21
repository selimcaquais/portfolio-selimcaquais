<template>
    <!-- <div class="cursor"></div> -->
    <div class="circleCursor"></div>
</template>

<script setup>
import { onMounted, onBeforeUnmount } from 'vue';

onMounted(() => {
    // const cursor = document.querySelector(".cursor"); 
    const circleCursor = document.querySelector(".circleCursor"); 

    const updateCursorPosition = (event) => {
        // cursor.style.top = `${event.clientY - 2}px`;
        // cursor.style.left = `${event.clientX - 2}px`;
        circleCursor.style.top = `${event.clientY - 24}px`;
        circleCursor.style.left = `${event.clientX - 24}px`;
    };

    window.addEventListener('mousemove', updateCursorPosition);

    onBeforeUnmount(() => {
        window.removeEventListener('mousemove', updateCursorPosition);
    });
});
</script>

<style>
    /* .cursor{
        position: absolute;
        width: 0.3em;
        height: 0.3em;
        background-color: #000;
        z-index: 30;
        border-radius: 100%;
        pointer-events: none;
    } */

    .circleCursor{
        position: absolute;
        width: 3em;
        height: 3em;
        z-index: 50;
        background-color: #fff;
        mix-blend-mode: difference;
        border-radius: 100%;
        border: 1px solid white;
        pointer-events: none;
    }
</style>

