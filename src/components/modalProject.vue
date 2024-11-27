<script setup>
import { ref } from 'vue';
import ChevronLeftIcon from './icons/chevronLeftIcon.vue';
import CrossMarkIcon from './icons/crossMarkIcon.vue';
import arrowLeftTopIcon from './icons/arrowLeftTopIcon.vue';
import GithubLogoIcon from './icons/githubLogoIcon.vue';

const props = defineProps({
  actualProject: { required: true },
});

const imageIndex = ref(0);

const emit = defineEmits(['close']);

const closeModal = () => {
  emit('close');
};

const handleImageIndexPlus = () =>{
  imageIndex.value = (imageIndex.value + 1) % props.actualProject.images.length;
}
const handleImageIndexMinus = () =>{
  imageIndex.value = (imageIndex.value - 1 + props.actualProject.images.length) % props.actualProject.images.length;
}

</script>
<template>
    <div class="modalProject">

      <div class="flex justify-end">
        <button @click="closeModal" class="cursor-none">
          <CrossMarkIcon class="w-12 p-2 stroke-white transition-transform duration-300 hover:rotate-90"/>
        </button>
      </div>

      <h2 class=" font-archivoBlack text-white text-7xl pl-24">{{ (actualProject.title).toUpperCase() }}</h2>

      <p class="font-archivo text-white pt-12 w-2/3 pl-24">{{ actualProject.description }}</p>
      
      <div class="flex justify-center items-center pt-12 gap-12">
        <ChevronLeftIcon class="w-8 f-git stroke-white transition-transform duration-200 hover:scale-125" @click="handleImageIndexMinus"/>
        <img loading="lazy" :src="actualProject.images[imageIndex]" class="w-[40em] h-[25em] object-cover select-none"/>
        <ChevronLeftIcon class="transform stroke-white rotate-180 w-8 h-fit  transition-transform duration-200 hover:scale-125" @click="handleImageIndexPlus"/>
      </div>


      <div class="flex flex-col items-center justify-center gap-2 pt-6">
        <a href="" v-if="actualProject.linkToTheGithub" class="linkedProject inline-block group cursor-none">
        <div class="flex gap-2 p-2">
                <p class="font-archivo">Github</p>
                <GithubLogoIcon class="fill-primary block transition-all delay-[250ms] ease-out w-0 group-hover:w-6"/>
            </div>
        </a>

        <a href="" v-if="actualProject.linkToTheProject" class="linkedProject inline-block group cursor-none">
        <div class="flex gap-2">
                <p class="font-archivo">Accéder au projet</p>
                <arrowLeftTopIcon class="stroke-primary block transition-all delay-[250ms] ease-out w-0 group-hover:w-4"/>
            </div>
        </a>
      </div>
    </div>
</template>

<style>

.modalProject{
  position: absolute;
  display: block;
  z-index: 40;

  width: 92vw;
  height: 92vh;

  top: 4vh;
  left: 4vw;

  background: rgba(255, 255, 255, 0.1);
  border-radius: 16px;
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border: 1px solid rgba(255, 255, 255, 0.3);

  padding:1em;

  animation: modalAppearance 0.2s ease-in-out forwards;
}

@keyframes modalAppearance {
        from {
            top:35vh;
            border-radius: 25rem 25rem 1rem 1rem;
            transform: scale(0);
        }
        
        to {
            top:4vh;
            border: 1px solid rgba(255, 255, 255, 0.3);
            transform: scale(1);
        }
    }

  .linkedProject {
    background-image: linear-gradient(
      to left,
      #fff,
      #fff 50%,
      #FFB907 50%
    );
    background-size: 200% 100%;
    background-position: 100%;
    display: inline-block;
    padding: 5px 0;
    position: relative;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    transition: all 0.3s ease-in-out;
  }
  
  .linkedProject:before{
    content: '';
    background: #FFB907;
    display: block;
    position: absolute;
    transition: all 0.3s ease-in-out;
  }
  
  .linkedProject:hover {
   background-position: 0;
  }
  
  .linkedProject:hover::before{
    width: 100%;
  }
</style>

