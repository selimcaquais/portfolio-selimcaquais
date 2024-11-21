<script setup>
import backgroundIframe from './components/background/backgroundIframe.vue';
import filterBackground from './components/background/filterBackground.vue';
import descritpionHero from './components/descritpionHero.vue';
import headshotPicture from './components/headshotPicture.vue';
import contactMainPage from './components/contactMainPage.vue';
import projectGallery from './components/projectGallery.vue';
import "./assets/css/main.css";
import mouseCursor from './components/background/mouseCursor.vue';
import modalProject from './components/modalProject.vue';
import { ref } from 'vue';

const isModalProjectOpen = ref(false); 
const actualProject = ref(null);

const handleModalOpen = (data) => {
  actualProject.value = data;
  isModalProjectOpen.value = true;
};

const closeModalProject = () => {
  const modal = document.querySelector('.modalProject')
  // animation remove modal
  modal.animate([{top:'4vh',border: '1px solid rgba(255, 255, 255, 0.3)', borderRadius: "25rem 1rem 1rem 1rem",transform: 'scale(1)'},
                 {top:"35vh",borderRadius: "25rem 25rem 1rem 1rem",transform: "scale(0)",}],
                 {duration:200});

  setTimeout(()=>{isModalProjectOpen.value = false},200);
};

</script>

<template>
  <mouseCursor/>


  <!-- Background  -->
   <div class="absolute w-screen h-screen overflow-hidden">
    <backgroundIframe/>
    <filterBackground/>
   </div>

   <!-- Modal Project -->

   <modalProject 
    v-if="isModalProjectOpen === true" 
    :actualProject="actualProject"
    @close="closeModalProject"/>

   <!-- Main Page -->
   <div class="absolute w-screen h-screen z-20">

    <!-- header and hero banner -->
      <div class="h-1/2 w-screen flex">
        <div class="w-2/3 h-full flex flex-col">

            <!-- header -->
            <div class="title-header-wrapper ml-8 mt-8 mr">
              <div class="flex flex-col w-min text-nowrap">
                <h1 class="text-primary font-archivoBlack text-8xl">SELIM CAQUAIS</h1>
                <h3 class="font-archivo text-white mr-2 place-self-end">Front-end developer</h3>
              </div>
            </div>

            <!-- description -->
            <div class="hero-description-wrapper flex items-center h-full w-2/3 pl-32 pt-24">
              <descritpionHero/>
            </div>
          </div>

          <div class="w-[17%] h-full flex items-center justify-center pt-24">
            <div class="w-2/3">
              <headshotPicture/>
            </div>
          </div>

          <div class="w-[17%] h-full pt-10 pr-8">
            <contactMainPage/>
          </div>
      </div>

      <div class="h-1/2 w-screen">
          <div class="h-[30%] w-full flex justify-end pr-8 align-center">
            <p class="text-white font-archivoBlack text-8xl">PROJETS</p>
          </div>
          <div class="h-[70%] w-full flex justify-center items-center">
            <projectGallery @open="handleModalOpen"/>
          </div>
      </div>

   </div>
</template>