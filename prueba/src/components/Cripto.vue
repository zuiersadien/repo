<script setup lang="ts">
import { number } from "@intlify/core-base";
import {defineProps, inject ,ref,defineEmits} from "vue"

defineProps({
valor:String
}
    
)
 const emit=defineEmits(["modificarValor"])
 

    const handleClose = (e) => {
        emit('modificarValor',e.target.value)
        
    }
</script>

<template>
fiat
    <div>

    <input type="text" :value="valor" v-on:keyup="handleClose">

</div>



</template>

<style scoped lang="scss">

</style>