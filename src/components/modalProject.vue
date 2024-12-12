<script setup>
import { onMounted } from 'vue';
import CrossMarkIcon from './icons/crossMarkIcon.vue';
import arrowLeftTopIcon from './icons/arrowLeftTopIcon.vue';
import GithubLogoIcon from './icons/githubLogoIcon.vue';

const props = defineProps({
  actualProject: { required: true },
  isModalProjectOpen: {required:true},
});

const emit = defineEmits(['close']);

const closeModal = () => {
  emit('close');
};

onMounted (() => {
  const carouselList = document.querySelector('.carousel__list');
  const carouselItems = document.querySelectorAll('.carousel__item');
  const elems = Array.from(carouselItems);

let isThrottled = false;

const handleScroll = (event) => {
  if (isThrottled) return;
  isThrottled = true;

  setTimeout(() => {
    isThrottled = false; 
  }, 2200);

  const direction = event.deltaX > 0 ? 1 : -1;

  // Trouve le nouvel élément actif en fonction de la direction
  const current = elems.find((elem) => elem.dataset.pos == 0);
  const currentIndex = elems.indexOf(current);

  const newActiveIndex = (currentIndex + direction + elems.length) % elems.length;

  const newActive = elems[newActiveIndex];
  update(newActive);
};

window.addEventListener('wheel', handleScroll);

carouselList.addEventListener('click', function (event) {
  var newActive = event.target;
  var isItem = newActive.closest('.carousel__item');

  if (!isItem || newActive.classList.contains('carousel__item_active')) {
    return;
  };
  
  update(newActive);
});

const update = function(newActive) {
  const newActivePos = newActive.dataset.pos;

  const current = elems.find((elem) => elem.dataset.pos == 0);
  const prev = elems.find((elem) => elem.dataset.pos == -1);
  const next = elems.find((elem) => elem.dataset.pos == 1);
  const first = elems.find((elem) => elem.dataset.pos == -2);
  const last = elems.find((elem) => elem.dataset.pos == 2);

  current.classList.remove('carousel__item_active');
  
  [current, prev, next, first, last].forEach(item => {
    var itemPos = item.dataset.pos;

    item.dataset.pos = getPos(itemPos, newActivePos)
  });
};

const getPos = function (current, active) {
  const diff = current - active;

  if (Math.abs(current - active) > 2) {
    return -current
  }

  return diff;
}
});
  
</script>

<template>
    <div class="modalProject">

      <div class="flex justify-end">
        <button @click="closeModal" class="cursor-none">
          <CrossMarkIcon class="w-12 p-2 stroke-white transition-transform duration-300 hover:rotate-90"/>
        </button>
      </div>

      <h2 class=" font-archivoBlack text-white text-7xl pl-24">{{ (props.actualProject.title).toUpperCase() }}</h2>

      <p class="font-archivo text-white pt-12 w-2/3 pl-24">{{ props.actualProject.description }}</p>
      
      <div class="flex justify-center items-center gap-12">
          <ul class="carousel__list">
            <li v-for="image in props.actualProject.images" 
                v-bind:key="(props.actualProject.images).indexOf(image)+1" 
                class="carousel__item" 
                :data-pos="((props.actualProject.images).indexOf(image)+1) - 3">
                <img class="pointer-events-none h-full" :src="image" alt="">
              </li>
          </ul>
      </div>

      <div class="flex flex-col items-center justify-center gap-2 pt-6">
        <a href="" v-if="props.actualProject.linkToTheGithub" class="linkedProject inline-block group cursor-none">
        <div class="flex gap-2 p-2">
                <a class="font-archivo cursor-none" :href="props.actualProject.linkToTheGithub" target="_blank">Github</a>
                <GithubLogoIcon class="fill-primary block transition-all delay-[250ms] ease-out w-0 group-hover:w-6"/>
            </div>
        </a>

        <a href="" v-if="props.actualProject.linkToTheProject" class="linkedProject inline-block group cursor-none">
        <div class="flex gap-2">
                <a class="font-archivo cursor-none" :href="props.actualProject.linkToTheProject" target="_blank">Accéder au projet</a>
                <arrowLeftTopIcon class="stroke-primary block transition-all delay-[250ms] ease-out w-0 group-hover:w-4"/>
            </div>
        </a>
      </div>

    </div>
</template>

<style>
.carousel__list {
    display: flex;
    list-style: none;
    position: relative;
    width: 100%;
    height:25rem; 
    justify-content: center;
    align-items: center;
    perspective: 300px;
}
  
.carousel__item {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 30rem;
    height: 20rem;
    background-color: rgba(0, 0, 0, 0.7);
    position: absolute;
    transition: all .3s ease-in;
}
.carousel__item:nth-child(1) {
      background-image:url("image/1.jpg");
      background-repeat: no-repeat;
      background-size: cover;
    }
.carousel__item:nth-child(2) {
      background-image:url("image/2.jpg");
      background-repeat: no-repeat;
      background-size: cover;
    }
.carousel__item:nth-child(3) {
      background-image:url("image/3.jpg");
      background-repeat: no-repeat;
      background-size: cover;
    }
.carousel__item:nth-child(4) {
      background-image:url("image/1.jpg");
      background-repeat: no-repeat;
      background-size: cover;
    }
.carousel__item:nth-child(5) {
      background-image:url("image/2.jpg");
      background-repeat: no-repeat;
      background-size: cover;
    }
    
.carousel__item[data-pos="0"] {
      z-index: 5;
    }
    
.carousel__item[data-pos="-1"],
.carousel__item[data-pos="1"] {
      opacity: 0.7;
      filter: blur(1px) grayscale(10%);
    }
    
.carousel__item[data-pos="-1"] {
      transform: translateX(-40%) scale(.9);
      z-index: 4;
    }
    
.carousel__item[data-pos="1"] {
      transform: translateX(40%) scale(.9);
      z-index: 4;
    }
    
.carousel__item[data-pos="-2"],
.carousel__item[data-pos="2"] {
      opacity: 0.4;
      filter: blur(3px) grayscale(20%);
    }
    
.carousel__item[data-pos="-2"] {
      transform: translateX(-70%) scale(.8);
      z-index: 3;
    }
    
.carousel__item[data-pos="2"] {
      transform: translateX(70%) scale(.8);
      z-index: 3;
    }
    
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
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
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

<script>

</script>