<script setup>
import backgroundIframe from './components/background/backgroundIframe.vue';
import filterBackground from './components/background/filterBackground.vue';
// import mouseCursor from './components/mouseCursor.vue';
import "./assets/main.css";

</script>

<template>
  <!-- <mouseCursor/> -->



  <!-- Background  -->
   <div class="absolute w-screen h-screen overflow-hidden">
    <backgroundIframe/>
    <filterBackground/>
   </div>

   <!-- Main Page -->
   <div class="absolute w-screen h-screen z-20">

    <!-- header and hero banner -->
      <div class="h-[55%] w-screen flex">
        <div class="w-2/3 h-full bg-blue-500">

            <!-- header -->
            <div class="title-header-wrapper ml-8 mt-8 mr">
              <div class="flex flex-col w-min text-nowrap">
                <h1 class="text-primary font-archivoBlack text-8xl">SELIM CAQUAIS</h1>
                <h3 class="font-archivo text-white mr-2 place-self-end">Front-end developer</h3>
              </div>
            </div>

            <!-- description -->
            <div class="hero-description-wrapper">
              <descritpionHero/>
            </div>
          </div>

          <div class="w-[17%] h-full bg-red-500">
            <imageHero/>
          </div>

          <div class="w-[17%] h-full bg-yellow-500">
            <contactMainPage/>
          </div>
      </div>

      <div class="h-[45%] w-screen">
          <div class="h-[30%] w-full bg-green-500">
            <h1></h1>
          </div>
          <div class="h-[70%] w-full bg-pink-500">
            <projectGallery/>
          </div>
      </div>

   </div>
</template>