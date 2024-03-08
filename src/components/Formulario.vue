<script setup>
import Input from './Input.vue';
import { ref } from 'vue';

const emit = defineEmits(['registrarCliente'])
//Escuchadores de eventos
//  Datos para los inputs
const inputsData = [
    {   
        nombre: "cliente",
        ingresar: "Nombre del Cliente",
        tipo: "text",
        msg:ref('')
    },
    {
        nombre: "electrodomestico",
        ingresar: "Electrodomestico Reparado",
        tipo: "text",
        msg:ref('')
    },
    {
        nombre: "direccion",
        ingresar: "Direccion del Cliente",
        tipo: "text",
        msg:ref('')
    },
    {
        nombre: "localidad",
        ingresar: "Localidad Del Cliente",
        tipo: "text",
        msg:ref('')
    },
    {
        nombre: "fecha",
        ingresar: "Fecha de Reparación",
        tipo: "date",
        msg:ref('')
    }
]

//Funciones
const leerInformacionDelMensaje = (mensaje,index) => {
  inputsData[index].msg.value = mensaje;
}

const enviarInformacion = () => {
    emit('registrarCliente',inputsData);
}

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
        <!--Formulario-->
        <form class="bg-white ml-5 shadow-md rounded-lg py-10 px-5 mb-10" v-on:submit.prevent="enviarInformacion">
            <!--Campos de los inputs del formulario-->
            <div v-for="(inputData , index) in inputsData" class="mb-5">
                <Input v-on:leer-informacion="(mensaje) => leerInformacionDelMensaje (mensaje,index)" v-bind:inputData="inputData"/>
                <!--Componente input-->
            </div>
            <div>
                <!--Input para enviar la información-->
                <button type="submit" class="bg-red-600 p-3
                text-white uppercase font-bold 
                hover:bg-red-700 cursor-pointer transition-colors">Enviar información</button>
            </div>
        </form>
        <!--Fin del formulario-->
    </div>
</template>

<style></style>