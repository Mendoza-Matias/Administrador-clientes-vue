<script setup>
import { computed } from 'vue'
const props = defineProps(['alerta'])

/*Logica necesaria */
const isError = computed(() => {
     props.alerta.tipo === "error"
})

</script>
<template>
    <div :class="[isError ? 'bg-red-500' : 'bg-green-500']" 
    class="text-center text-white p-3 uppercase font-bold mb-3  rounded-md">
        {{ props.alerta.mensaje }}
    </div>
</template>
<style lang="">
    
</style>