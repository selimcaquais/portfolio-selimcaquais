<script setup>
import ArrowLeft from './icons/arrowLeftIcon.vue';
import CalendarIcon from './icons/calendarIcon.vue';

</script>

<template>
    <div class="text-white font-archivo">
        <h3 class="font-archivoBlack pb-4">Qui suis-je ?</h3>
        <p class="pb-4">
            Lorem Ipsum is simply dummy text of the printing and typesetting industry. 
            Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, 
            when an unknown printer took a galley of type and scrambled it to make a type specimen book. 
            It has survived not only five centuries, but also the leap into electronic typesetting, 
            remaining essentially unchanged.
        </p>
        <a href="#" class="inline-block cursor-none">
            <button class="border rounded-full cursor-none p-2 flex gap-1 group items-center transition-all duration-300 hover:pr-4 hover:text-primary hover:border-primary">
                Prendre rendez-vous
                <CalendarIcon class="block transition-all duration-300 ease-out w-0 h-6 group-hover:w-6 group-hover:ml-2"/>
                <ArrowLeft class="w-6 h-6 transition-transform duration-300 transform group-hover:translate-x-2"/>
            </button>
        </a>
    </div>
</template>


<style>
</style>