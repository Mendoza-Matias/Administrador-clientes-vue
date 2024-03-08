<script setup>
import { ref } from 'vue';
const erroInput = ref('');
//Escuchadores de eventos
//Props
defineProps({
    inputData: {
        type: Object
    }
})
//Eventos
const emit = defineEmits(['leerInformacion'])

//Funciones
const obtenerInformacion = (event) => {
    if (event.target.value === '') {
        erroInput.value = 'No puedo estar vacio';
    } else {
        erroInput.value = ''
    }
    emit('leerInformacion', event.target.value); //puedo validar en tiempo real a medida que el usuario va a escribiendo.
    //validar con el target
}
</script>

<template>
    <!--Input-->
    <label :for='inputData.nombre' class="block text-gray-700 uppercase font-bold">
        {{ inputData.ingresar }}
    </label>
    <input v-on:input="obtenerInformacion" :id='inputData.nombre' :type='inputData.tipo'
        :placeholder='inputData.ingresar' class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md">
    <small>{{ erroInput }}</small>
</template>

<style></style>