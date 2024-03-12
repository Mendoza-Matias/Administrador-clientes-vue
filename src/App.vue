<script setup>
import { ref } from 'vue'
import {uid} from 'uid'
import Header from './components/Header.vue'
import Formulario from './components/Formulario.vue'
import Cliente from './components/Cliente.vue'

const clientes = ref([]);
const clienteEditado = ref([])

const recibirCliente = (cliente) => {
    cliente.id = uid()
    clientes.value.push(cliente);
}

const actualizarCliente = (id) =>{
    clienteEditado.value = clientes.value.filter(cliente => cliente.id === id)[0]
}

const eliminarCliente = () => {
    console.log("eliminar")
}

</script>

<template>
    <div class="container mx-auto mt-20">
        <Header />
    </div>
    <div class="mt-12 md:flex">
        <Formulario v-on:registrarCliente="recibirCliente" :clientes="clientes" :clienteEditado="clienteEditado"/>
        <div class="md:w-1/2 md:h-screen overflow-y-scroll">
            <h3 class="font-black text-3xl text-center">Administrar a tus Clientes</h3>
            <!--Parrafo-->
            <p class="text-lg mt-5 text-center mb-10">
                Clientes para
                <span class="text-red-600 font-bold">Adminístrar</span>
            </p>
            <div>
                <Cliente v-on:actualizar-cliente="actualizarCliente" 
                v-on:eliminar-cliente="eliminarCliente" 
                v-for="(cliente, indice) in clientes" 
                v-bind:cliente="cliente" v-bind:indice="indice" />
            </div>
            <!-- <p class="text-center mt-20 text-2xl">No hay clientes para administrar.</p> -->
        </div>
    </div>
</template>

<style scoped></style>
