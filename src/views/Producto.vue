<template>
  <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-10 min-h-screen bg-gray-50">
    
    <div class="mb-8">
      <h1 class="text-3xl font-extrabold text-gray-900 tracking-tight">
        Gestión de Productos
      </h1>
      <p class="mt-2 text-sm text-gray-600">
        Crea, edita o elimina los productos de tu inventario en tiempo real.
      </p>
    </div>

    <div class="grid grid-cols-1 lg:grid-cols-3 gap-8 items-start">
      
      <div class="bg-white rounded-2xl p-6 shadow-sm border border-gray-100 lg:sticky lg:top-24">
        <h2 class="text-lg font-bold text-gray-800 mb-6 flex items-center gap-2">
          <span class="w-2 h-5 bg-indigo-600 rounded-full block"></span>
          Información del Producto
        </h2>
        
        <div class="space-y-4">
          <div>
            <label for="nombre" class="block text-xs font-semibold text-gray-500 uppercase tracking-wider mb-1">Nombre</label>
            <input 
              type="text" 
              id="nombre" 
              v-model="producto.nombre" 
              placeholder="Ej. Silla Ergonómica"
              class="w-full px-4 py-2.5 rounded-xl border border-gray-200 text-gray-800 text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500/20 focus:border-indigo-500 transition-colors"
            />
          </div>

          <div class="grid grid-cols-2 gap-4">
            <div>
              <label for="stock" class="block text-xs font-semibold text-gray-500 uppercase tracking-wider mb-1">Stock</label>
              <input 
                type="number" 
                id="stock" 
                v-model="producto.stock" 
                placeholder="0"
                class="w-full px-4 py-2.5 rounded-xl border border-gray-200 text-gray-800 text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500/20 focus:border-indigo-500 transition-colors"
              />
            </div>
            <div>
              <label for="precio" class="block text-xs font-semibold text-gray-500 uppercase tracking-wider mb-1">Precio</label>
              <input 
                type="number" 
                id="precio" 
                v-model="producto.precio" 
                placeholder="0.00"
                class="w-full px-4 py-2.5 rounded-xl border border-gray-200 text-gray-800 text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500/20 focus:border-indigo-500 transition-colors"
              />
            </div>
          </div>

          <div>
            <label for="imagen" class="block text-xs font-semibold text-gray-500 uppercase tracking-wider mb-1">URL de la Imagen</label>
            <input 
              type="text" 
              id="imagen" 
              v-model="producto.imagen" 
              placeholder="https://ejemplo.com/imagen.jpg"
              class="w-full px-4 py-2.5 rounded-xl border border-gray-200 text-gray-800 text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500/20 focus:border-indigo-500 transition-colors"
            />
          </div>

          <button 
            @click="funGuardarProducto()"
            class="w-full mt-2 px-4 py-3 bg-indigo-600 hover:bg-indigo-700 text-white font-semibold text-sm rounded-xl shadow-sm hover:shadow transition-all duration-200 cursor-pointer"
          >
            Guardar Producto
          </button>
        </div>
      </div>


      <div class="lg:col-span-2 bg-white rounded-2xl shadow-sm border border-gray-100 overflow-hidden">
        <div class="overflow-x-auto">
          <table class="w-full text-left border-collapse">
            <thead>
              <tr class="bg-gray-50/70 border-b border-gray-100">
                <th class="px-6 py-4 text-xs font-bold text-gray-500 uppercase tracking-wider">Producto</th>
                <th class="px-6 py-4 text-xs font-bold text-gray-500 uppercase tracking-wider text-center">Stock</th>
                <th class="px-6 py-4 text-xs font-bold text-gray-500 uppercase tracking-wider text-right">Precio</th>
                <th class="px-6 py-4 text-xs font-bold text-gray-500 uppercase tracking-wider text-right">Acciones</th>
              </tr>
            </thead>
            <tbody class="divide-y divide-gray-100">
              <tr v-if="productos.length === 0">
                <td colspan="4" class="px-6 py-10 text-center text-sm text-gray-400 italic">
                  No hay productos registrados aún.
                </td>
              </tr>

              <tr 
                v-for="(prod, posicion) in productos" 
                :key="posicion"
                class="hover:bg-gray-50/50 transition-colors"
              >
                <td class="px-6 py-4 whitespace-nowrap">
                  <div class="flex items-center gap-4">
                    <div class="w-12 h-12 rounded-xl bg-gray-100 border border-gray-100 overflow-hidden flex-shrink-0">
                      <img 
                        :src="prod.imagen || 'https://images.unsplash.com/photo-1531403009284-440f080d1e12?auto=format&fit=crop&w=100&q=80'" 
                        alt="Imagen del producto" 
                        class="w-full h-full object-cover"
                      />
                    </div>
                    <div class="font-semibold text-gray-800 text-sm">
                      {{ prod.nombre }}
                    </div>
                  </div>
                </td>

                <td class="px-6 py-4 whitespace-nowrap text-center">
                  <span 
                    class="px-2.5 py-1 rounded-full text-xs font-bold"
                    :class="prod.stock > 0 ? 'bg-emerald-50 text-emerald-700' : 'bg-rose-50 text-rose-700'"
                  >
                    {{ prod.stock }} u.
                  </span>
                </td>

                <td class="px-6 py-4 whitespace-nowrap text-right font-black text-gray-900 text-sm">
                  ${{ prod.precio }}
                </td>

                <td class="px-6 py-4 whitespace-nowrap text-right text-sm font-medium">
                  <div class="flex items-center justify-end gap-2">
                    <button 
                      @click="funEditar(prod)"
                      class="px-3 py-1.5 rounded-lg text-xs font-bold text-indigo-600 hover:bg-indigo-50 transition-colors cursor-pointer"
                    >
                      Editar
                    </button>
                    <button 
                      @click="funEliminar(posicion)"
                      class="px-3 py-1.5 rounded-lg text-xs font-bold text-rose-600 hover:bg-rose-50 transition-colors cursor-pointer"
                    >
                      Eliminar
                    </button>
                  </div>
                </td>

              </tr>
            </tbody>
          </table>
        </div>
      </div>

    </div>
  </div>
</template>

<script setup>
    import { onMounted, ref } from 'vue'
    
    const productos = ref([]);
    const producto = ref({});
    const edicion = ref(false)

    onMounted(() => {
        // alert("Cargando Producto...")
        funListar()
    });

    function funListar(){
        const datos = localStorage.getItem("productos") || "[]";
        productos.value = JSON.parse(datos);
    }

    function funGuardarProducto(){
        if(edicion.value){
            producto.value = {}
            edicion.value = false;
        }else{
            const nuevoProd = producto.value
            productos.value.push(nuevoProd);
            producto.value = {}

        }
        localStorage.setItem("productos", JSON.stringify(productos.value))
        
    }

    function funEditar(prod){
        edicion.value = true;
        producto.value = prod;
        
    }

    function funEliminar(posicion){
        productos.value.splice(posicion, 1);
    }


</script>