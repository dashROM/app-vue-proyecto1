<template>
  <div class="min-h-screen bg-gray-100 p-8">
    <!-- Título -->
    <h1 class="text-4xl font-bold text-center text-gray-800 mb-8">
      🛍️ Catálogo de Productos
    </h1>

    <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">

      <!-- ===================== PRODUCTOS ===================== -->
      <div class="lg:col-span-2">
        <div class="grid grid-cols-1 sm:grid-cols-2 xl:grid-cols-3 gap-6">

          <div
            v-for="prod in productos"
            :key="prod.nombre"
            class="bg-white rounded-xl shadow-md hover:shadow-xl transition overflow-hidden"
          >
            <!-- Imagen -->
            <img
              :src="prod.imagen"
              :alt="prod.nombre"
              class="w-full h-56 object-cover"
            />

            <!-- Información -->
            <div class="p-5">

              <h2 class="text-lg font-bold text-gray-800">
                {{ prod.nombre }}
              </h2>

              <p class="text-2xl font-bold text-green-600 mt-2">
                Bs. {{ prod.precio }}
              </p>

              <button
                @click="agregaCarrito(prod)"
                class="mt-5 w-full bg-blue-600 hover:bg-blue-700 text-white py-2 rounded-lg transition"
              >
                🛒 Añadir al carrito
              </button>

            </div>
          </div>

        </div>
      </div>

      <!-- ===================== CARRITO ===================== -->
      <div class="bg-white rounded-xl shadow-lg p-6 h-fit sticky top-5">

        <h2 class="text-2xl font-bold mb-5">
          🛒 Carrito de Compras
        </h2>

        <div
          v-if="carrito.length === 0"
          class="text-center text-gray-500 py-10"
        >
          No hay productos en el carrito.
        </div>

        <div
          v-for="item in carrito"
          :key="item.nombre"
          class="border-b py-4 flex gap-4"
        >

          <!-- Imagen -->
          <img
            :src="item.imagen"
            :alt="item.nombre"
            class="w-20 h-20 object-cover rounded-lg border"
          />

          <div class="flex-1">

            <div class="flex justify-between">

              <div>
                <h3 class="font-semibold">
                  {{ item.nombre }}
                </h3>

                <p class="text-sm text-gray-500">
                  Bs. {{ item.precio }} c/u
                </p>
              </div>

              <span class="font-bold text-green-600">
                Bs. {{ item.precio * item.cantidad }}
              </span>

            </div>

            <div class="flex items-center gap-2 mt-3">

              <button
                @click="disminuir(item)"
                class="bg-red-500 hover:bg-red-600 text-white w-8 h-8 rounded"
              >
                -
              </button>

              <span class="font-bold w-6 text-center">
                {{ item.cantidad }}
              </span>

              <button
                @click="aumentar(item)"
                class="bg-green-500 hover:bg-green-600 text-white w-8 h-8 rounded"
              >
                +
              </button>

              <button
                @click="eliminar(item)"
                class="ml-auto bg-gray-700 hover:bg-black text-white px-3 py-1 rounded"
              >
                Eliminar
              </button>

            </div>

          </div>

        </div>

        <!-- Total -->
        <div
          v-if="carrito.length"
          class="mt-6 border-t pt-4"
        >

          <div class="flex justify-between text-xl font-bold">
            <span>Total</span>

            <span class="text-blue-600">
              Bs. {{ total }}
            </span>
          </div>

          <button
            class="mt-5 w-full bg-emerald-600 hover:bg-emerald-700 text-white py-3 rounded-lg font-semibold"
          >
            Finalizar Compra
          </button>

        </div>

      </div>

    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, watch } from "vue";

const productos = ref([]);
const carrito = ref([]);

// Cargar datos
onMounted(() => {
  productos.value = JSON.parse(localStorage.getItem("productos") || "[]");
  carrito.value = JSON.parse(localStorage.getItem("carrito") || "[]");
});

// Guardar automáticamente el carrito
watch(
  carrito,
  (nuevoCarrito) => {
    localStorage.setItem("carrito", JSON.stringify(nuevoCarrito));
  },
  { deep: true }
);

// Agregar al carrito
function agregaCarrito(prod) {
  const existe = carrito.value.find(
    item => item.nombre === prod.nombre
  );

  if (existe) {
    existe.cantidad++;
  } else {
    carrito.value.push({
      nombre: prod.nombre,
      precio: Number(prod.precio),
      imagen: prod.imagen,
      cantidad: 1
    });
  }
}

// Aumentar cantidad
function aumentar(item) {
  item.cantidad++;
}

// Disminuir cantidad
function disminuir(item) {
  if (item.cantidad > 1) {
    item.cantidad--;
  } else {
    eliminar(item);
  }
}

// Eliminar producto
function eliminar(item) {
  carrito.value = carrito.value.filter(
    p => p.nombre !== item.nombre
  );
}

// Vaciar carrito (opcional)
function vaciarCarrito() {
  carrito.value = [];
}

// Total
const total = computed(() =>
  carrito.value.reduce(
    (suma, item) => suma + item.precio * item.cantidad,
    0
  )
);
</script>