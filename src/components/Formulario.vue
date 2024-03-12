<script setup>
import { reactive, computed } from 'vue'
import Alerta from './Alerta.vue'

const props = defineProps({
    id: {
        type: [String, null]
    },
    nombre: {
        type: String
    },
    reparacion: {
        type: String
    },
    direccion: {
        type: String
    },
    localidad: {
        type: String
    },
    fecha: {
        type: String
    }
})

const alerta = reactive({
    tipo: "", /*Exito|Error*/
    mensaje: "" /*Mensaje */
});

//Emisores
const emit = defineEmits([
    'update:nombre',
    'update:reparacion',
    'update:direccion',
    'update:localidad',
    'update:fecha',
    'guardarCliente'])

//Funciones
const enviarInformacion = () => {
    if (Object.values(props).includes("")) {
        alerta.tipo = "error"
        alerta.mensaje = "Todos los campos son obligatorios"
        return;
    }
    emit('guardarCliente'); //Envio el evento una ves pasada la validación
    alerta.tipo = "exito"
    alerta.mensaje = "Información enviada"
    setTimeout(() => {
        Object.assign(alerta, {
            tipo: "",
            mensaje: ""
        })
    }, 3000)
}

const editando = computed(() => {
    return props.id;
})

</script>
<template>
    <!--HTML-->
    <div class="md:w-1/2">
        <h2 class="font-black text-3xl text-center">Seguimiento Clientes</h2>
        <!--Parrafo-->
        <p class="text-lg mt-5 text-center mb-10">
            Añade un Cliente y
            <span class="text-red-600 font-bold">Adminístralo</span>
        </p>
        <!--Fin del parrafo-->
        <!--Alerta-->
        <div>
            <Alerta v-if="alerta.mensaje" v-bind:alerta="alerta" />
        </div>
        <!--Formulario-->
        <form class="bg-white ml-5 shadow-md rounded-lg py-10 px-5 mb-10" v-on:submit.prevent="enviarInformacion">
            <!--v-on: siempre es para eventos || simplificado @submit.prevent-->
            <!--Input-->
            <div class="mb-5">
                <label for="cliente" class="block text-gray-700 uppercase font-bold">
                    Nombre
                </label>
                <!--v-model simplifica el (e) -> -->
                <input v-on:input="$emit('update:nombre', $event.target.value)" id="cliente" type="text"
                    placeholder="Nombre del cliente" class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    :value="nombre">
            </div>
            <!--Input-->
            <div class="mb-5">
                <label for="reparacion" class="block text-gray-700 uppercase font-bold">
                    Reparación
                </label>
                <input v-on:input="$emit('update:reparacion', $event.target.value)" id="reparacion" type="text"
                    placeholder="Reparación" class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    :value="reparacion">
            </div>
            <!--Input-->
            <div class="mb-5">
                <label for="direccion" class="block text-gray-700 uppercase font-bold">
                    Dirección
                </label>
                <input v-on:input="$emit('update:direccion', $event.target.value)" id="direccion" type="text"
                    placeholder="Dirección" class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    :value="direccion">
            </div>
            <!--Input-->
            <div class="mb-5">
                <label for="localidad" class="block text-gray-700 uppercase font-bold">
                    Localidad
                </label>
                <input v-on:input="$emit('update:localidad', $event.target.value)" id="localidad" type="text"
                    placeholder="Localidad" class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    :value="localidad">

            </div>
            <!--Input-->
            <div class="mb-5">
                <label for="fecha" class="block text-gray-700 uppercase font-bold">
                    Fecha
                </label>
                <input v-on:input="$emit('update:fecha', $event.target.value)" id="fecha" type="date" :value="fecha"
                    placeholder="Fecha" class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md">
            </div>
            <div>
                <!--Input para enviar la información-->
                <input type="submit" class="bg-red-600 p-3
                text-white uppercase font-bold 
                hover:bg-red-700 cursor-pointer transition-colors"
                    :value="[editando ? 'Guardar cambios':'Enviar información']" />
            </div>
        </form>
        <!--Fin del formulario-->
    </div>
</template>

<style></style>