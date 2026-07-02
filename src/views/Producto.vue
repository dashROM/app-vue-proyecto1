<template>
    <h1>Nuestros Productos</h1>
    <!-- <h3>El producto {{ producto }}</h3>
    <h3>Lista de Productos </h3> {{ productos }} -->

    <div>
        <label for="nombre">Nombre: </label>
        <input type="text" id="nombre" v-model="producto.nombre" />
        <br>
        <label for="stock">Stock: </label>
        <input type="number" id="stock" v-model="producto.stock" />
        <br>
        <label for="precio">Precio: </label>
        <input type="number" id="precio" v-model="producto.precio" />
        <br>
        <label for="imagen">Imagen: </label>
        <input type="text" id="imagen" v-model="producto.imagen" />
        <br>
        <button @click="funGuardarProducto()">Guardar Producto</button>
    </div>

    <table border="1">
        <thead>
            <tr>
                <th>Nombre</th>
                <th>Stock</th>
                <th>Precio</th>
                <th>Imagen</th>
                <th></th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="(prod, posicion) in productos">
                <td>{{ prod.nombre }}</td>
                <td>{{ prod.stock }}</td>
                <td>{{ prod.precio }}</td>
                <td><img :src="prod.imagen" alt="Imagen del producto" width="100" /></td>
                <td>
                    <button @click="funEditar(prod)">Editar</button>
                    <button @click="funEliminar(posicion)">Eliminar</button>
                </td>
            </tr>
        </tbody>   
    </table> 
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