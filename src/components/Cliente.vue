<script setup>
defineEmits(['actualizarCliente','eliminarCliente']);
defineProps({
    cliente: {
        type: Object
    },
    indice: {
        type: Number
    }
});
</script>
<template>
    <div class="mx-5 my-10 bg-white shadow-md px-5 py-10 rounded-xl">
        <p class="font-bold mb-3 text-gray-700 uppercase">Id:
            <span class="font-normal normal-case">
                {{ cliente.id }}
            </span>
        </p>
        <p class="font-bold mb-3 text-gray-700 uppercase">Nombre:
            <span class="font-normal normal-case">
                {{ cliente[0].msg }}
            </span>
        </p>

        <p class="font-bold mb-3 text-gray-700 uppercase">Electrodomestico Reparado:
            <span class="font-normal normal-case">
                {{ cliente[1].msg }}
            </span>
        </p>
        <p class="font-bold mb-3 text-gray-700 uppercase">Dirección:
            <span class="font-normal normal-case">
                {{ cliente[2].msg }}
            </span>
        </p>
        <p class="font-bold mb-3 text-gray-700 uppercase">Localidad:
            <span class="font-normal normal-case">
                {{ cliente[3].msg }}
            </span>
        </p>
        <p class="font-bold mb-3 text-gray-700 uppercase">Fecha:
            <span class="font-normal normal-case">
                {{ cliente[4].msg }}
            </span>
        </p>

        <div class="grid md:grid-cols-2  gap-5 mt-10 ">
            <button type="button" v-on:click="$emit('actualizarCliente', cliente.id)"
                class="block w-full py-2 px-10 bg-indigo-600 hover:bg-indigo-700 text-white font-bold uppercase rounded-lg">Editar</button>

            <button type="button" v-on:click="$emit('eliminarCliente')"
                class="block w-full py-2 px-10 bg-red-600 hover:bg-red-700 text-white font-bold uppercase rounded-lg">Eliminar</button>
        </div>
    </div>
</template>
<style></style>