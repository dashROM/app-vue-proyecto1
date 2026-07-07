<template>
  <nav class="bg-white border-b border-gray-100 sticky top-0 z-50 backdrop-blur-md bg-white/90">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex items-center justify-between h-16">
        
        <div class="flex-shrink-0">
          <RouterLink to="/" class="text-xl font-black tracking-wider text-indigo-600 hover:text-indigo-700 transition-colors">
            MI_MARCA
          </RouterLink>
        </div>

        <div class="flex space-x-1 sm:space-x-4 items-center">
          <RouterLink 
            to="/" 
            class="px-3 py-2 rounded-lg text-sm font-medium text-gray-600 hover:text-indigo-600 hover:bg-gray-50 transition-all duration-200"
            active-class="text-indigo-600 bg-indigo-50/70 font-semibold"
          >
            INICIO
          </RouterLink>

          <RouterLink 
            to="/producto" 
            class="px-3 py-2 rounded-lg text-sm font-medium text-gray-600 hover:text-indigo-600 hover:bg-gray-50 transition-all duration-200"
            active-class="text-indigo-600 bg-indigo-50/70 font-semibold"
          >
            PRODUCTOS
          </RouterLink>

          <RouterLink 
            to="/blog" 
            class="px-3 py-2 rounded-lg text-sm font-medium text-gray-600 hover:text-indigo-600 hover:bg-gray-50 transition-all duration-200"
            active-class="text-indigo-600 bg-indigo-50/70 font-semibold"
          >
            BLOG
          </RouterLink>

          <RouterLink 
            to="/productos-venta" 
            class="px-3 py-2 rounded-lg text-sm font-medium text-gray-600 hover:text-indigo-600 hover:bg-gray-50 transition-all duration-200"
            active-class="text-indigo-600 bg-indigo-50/70 font-semibold"
          >
            PRODUCTOS (VENTA)
          </RouterLink>

          <RouterLink 
            to="/login" 
            class="ml-2 px-4 py-2 rounded-xl text-sm font-semibold text-white bg-indigo-600 hover:bg-indigo-700 shadow-sm hover:shadow transition-all duration-200"
            active-class="bg-indigo-800 ring-2 ring-indigo-300"
          >
            INGRESAR
          </RouterLink>
        </div>

      </div>
    </div>
  </nav>

  <main class="min-h-screen bg-gray-50">
    <RouterView />
  </main>
</template>
