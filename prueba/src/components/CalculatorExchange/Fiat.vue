<script setup lang="ts">
import { number } from "@intlify/core-base";
import {defineProps, inject ,ref,defineEmits,onMounted} from "vue"
import IMask from 'imask';

defineProps({
valor:String
}
    
)
 const emit=defineEmits(["modificarValor"])
 

    const handleClose = (e) => {
        emit('modificarValor',e.target.value)
        
    }
onMounted(()=>{
    IMask(document.getElementById('phone-mask'), {
            mask: Number,
            decimal : ".",
            min: 0,
            max: 9999999,
        });

})
</script>

<template>
 <Field>
          <FieldLabel type="hero" label="Tu nos envías"></FieldLabel>
          <Control>
         <input class="input is-rounded size-lg" id="phone-mask"  rounded size="lg"  type="text" :value="valor" v-on:keyup="handleClose"/>

          </Control>
        </Field>

    <div>

</div>



</template>

<style scoped lang="scss">

</style>