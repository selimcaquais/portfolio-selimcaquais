<script setup>
import arrowLeftTopIcon from './icons/arrowLeftTopIcon.vue';

const links = [
    {title:'Github', links:'#'},
    {title:'Email', links:'#'},
    {title:'Malt', links:'#'},
    {title:'Linkedin', links:'#'}];
</script>

<template>
    <div class="flex flex-col items-end text-white gap-1 cursor-none">
        <p>Contactez moi</p>
        <hr class="h-px w-1/2">
        <a href="" v-for="link in links" v-bind:key="link.title" class="linked inline-block group cursor-none">
        <div class="flex">
                <p class="font-archivo">{{ link.title }} </p>
                <arrowLeftTopIcon class="stroke-primary block transition-all delay-[250ms] ease-out w-0 group-hover:w-4"/>
            </div>
        </a>
    </div>
</template>
<style>
.linked {
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
  
  .linked:before{
    content: '';
    background: #FFB907;
    display: block;
    position: absolute;
    transition: all 0.3s ease-in-out;
  }
  
  .linked:hover {
   background-position: 0;
  }
  
  .linked:hover::before{
    width: 100%;
  }
</style>