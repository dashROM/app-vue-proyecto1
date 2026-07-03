<template>
  <div class="min-h-screen bg-gray-50 py-10 px-4 sm:px-6 lg:px-8">
    
    <h1 class="text-4xl font-extrabold text-gray-900 text-center mb-12 tracking-tight">
      Nuestro Blog
    </h1>
    
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8 max-w-7xl mx-auto">
      
      <div 
        v-for="publi in publicaciones" 
        :key="publi.id" 
        class="bg-white rounded-2xl overflow-hidden shadow-md hover:shadow-xl transition-shadow duration-300 ease-in-out border border-gray-100 flex flex-col"
      >
        <div class="relative h-48 w-full overflow-hidden bg-gray-200">
          <img 
            :src="publi.cover_image" 
            :alt="publi.title"
            class="w-full h-full object-cover hover:scale-105 transition-transform duration-500 ease-in-out"
          />
        </div>

        <div class="p-6 flex flex-col flex-grow">
          <h2 class="text-xl font-bold text-gray-800 line-clamp-2 hover:text-indigo-600 transition-colors duration-200 mb-2">
            {{ publi.title }}
          </h2>
          
          <div class="mt-auto pt-4 border-t border-gray-50 flex items-center justify-between">
            <span class="text-sm font-medium text-gray-500">Precio</span>
            <p class="text-2xl font-black text-indigo-600">
              ${{ publi.precio }}
            </p>
          </div>
        </div>

      </div>
      </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue';

    const publicaciones = ref([]);

    onMounted(() => {
        obtenerDatosApiBackend();
    });

    function obtenerDatosApiBackend() {
        fetch('https://dev.to/api/articles')
            .then(response => response.json())
            .then(json => {
                publicaciones.value = json
            })
    }

</script> 