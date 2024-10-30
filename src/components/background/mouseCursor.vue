<template>
    <div class="cursor"></div>
</template>

<script setup>
import { onMounted, onBeforeUnmount } from 'vue';

onMounted(() => {
    const cursor = document.querySelector(".cursor"); 

    // Mettre à jour directement les coordonnées de la div dans l'événement 'mousemove'
    const updateCursorPosition = (event) => {
        cursor.style.top = `${event.clientY - 5}px`; // Ajuster pour centrer si nécessaire
        cursor.style.left = `${event.clientX - 5}px`;
    };

    // Ajouter l'écouteur de mouvement de la souris
    window.addEventListener('mousemove', updateCursorPosition);

    // Nettoyer l'écouteur au démontage
    onBeforeUnmount(() => {
        window.removeEventListener('mousemove', updateCursorPosition);
    });
});
</script>

<style>
    .cursor{
        position: absolute;
        width: 0.3em;
        height: 0.3em;
        background-color: #fff;
        z-index: 30;
        border-radius: 100%;
    }
</style>

