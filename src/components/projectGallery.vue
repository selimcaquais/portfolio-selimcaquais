<script setup>
import projects from "@/assets/data/projects.json";

</script>

<template>
  <!-- Wrapper des projets -->
  <div class="wrapper-projects w-screen mb-12 flex justify-center items-end gap-4 h-60 bottom-0">
    <div 
      class="project flex flex-col items-center justify-start" 
      v-for="project in projects" 
      :key="project.id" 
      :style="{ backgroundImage: `url(${project.imageButton})` }"
      @click="$emit('open', project);"
    >
       <p class="card-project mt-4 text-center font-archivoBlack" :style="{ color: project.color }">
            {{ project.title }}
        </p>
        <div class="absolute inset-0 flex items-center justify-center pointer-events-none">
            <p class="card-project text-center" :style="{ color: project.color2 }"> Click to see the project</p>
        </div>
    </div>
  </div>
</template>

<style>
.project {
  position: relative;
  height: 12em;
  width: 4em;
  color: #fff;
  background-position: center;
  background-size: auto 100%;
  background-repeat: no-repeat;
  transition: 0.5s, height 0.2s ease, width 0.3s ease 0.3s, filter 0.5s ease 0.3s; 
  filter: grayscale(100%);
}

.project:hover {
  height: 18em;
  width: 15em;
  filter: grayscale(0%);
}

.card-project {
  opacity: 0;
  overflow: hidden;
  transition: opacity 1s ease, width 0.5s ease;
}

.project:hover .card-project {
  opacity: 1;
}
</style>
