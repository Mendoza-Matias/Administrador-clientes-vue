<script setup>
import { uid } from 'uid'
import { ref, reactive, watch, onMounted } from 'vue'

/*Componentes */
import Header from './components/Header.vue'
import Formulario from './components/Formulario.vue'
import Cliente from './components/Cliente.vue'

const clientes = ref([]);
/*Si mi información va toda junta conviene un objeto reactive */
const cliente = reactive(
    {
        id: null,
        nombre: "",
        reparacion: "",
        direccion: "",
        localidad: "",
        fecha: ""
    }
)

watch(
    clientes, () => {
        guardarLocalStorage()
    },
    {
        deep: true
    }
)

const guardarLocalStorage = () => {
    localStorage.setItem('clientes', JSON.stringify(clientes.value));
}

// Cuando el componente esta listo carga la información
onMounted(() => { //Revisar si hay algo cuando cargue el componente
    const clientesStorage = localStorage.getItem('clientes')
    if (clientesStorage) {
        clientes.value = JSON.parse(clientesStorage); //Traigo la informacion del storage
    }
})

const guardarCliente = () => {
    if (cliente.id) {
        const { id } = cliente //Extraido el id
        //Obtengo el indice 
        const i = clientes.value.findIndex((clienteState) => clienteState.id === id)
        clientes.value[i] = {
            ...cliente,
            id: uid()
        }
    } else {
        clientes.value.push({
            ...cliente, //creo una copia que no es reactiva
            id: uid()
        });
        //Cargo la información de cliente en la lista.
    }
    //reiniciar objeto
    Object.assign(cliente, { //valores con los que se va a remplazar el objeto.

        nombre: "",
        reparacion: "",
        direccion: "",
        localidad: "",
        fecha: "",
        id: null
    })

}

const actualizarCliente = (id) => {
    const clienteEditar = (clientes.value.filter(cliente => cliente.id === id)[0]);
    Object.assign(cliente, clienteEditar)
}

const eliminarCliente = (id) => {
    console.log("eliminar")
    clientes.value = clientes.value.filter(cliente => cliente.id !== id);
}
</script>

<template>
    <div class="container mx-auto mt-20">
        <Header />
    </div>
    <div class="mt-12 md:flex">
        <!--Componente  || -->
        <Formulario v-model:nombre="cliente.nombre" v-model:reparacion="cliente.reparacion"
            v-model:direccion="cliente.direccion" v-model:localidad="cliente.localidad" v-model:fecha="cliente.fecha"
            v-on:guardar-cliente="guardarCliente" v-bind:id="cliente.id" />

        <!--Fin del componente-->
        <div class="md:w-1/2 md:h-screen overflow-y-scroll">
            <h3 class="font-black text-3xl text-center">Administrar a tus Clientes</h3>
            <!--Parrafo-->
            <p class="text-lg mt-5 text-center mb-10">
                Clientes para
                <span class="text-red-600 font-bold">Adminístrar</span>
            </p>

            <div v-if="clientes.length > 0">
                <Cliente v-on:actualizar-cliente="actualizarCliente" v-on:eliminar-cliente="eliminarCliente"
                    v-for="cliente in clientes" v-bind:cliente="cliente" />
            </div>
            <div v-else>
                <p class="mt-20 text-2xl text-center">No hay pacientes</p>
            </div>
        </div>
    </div>
</template>

<style scoped></style>
