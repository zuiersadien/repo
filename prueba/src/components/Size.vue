<script lang="ts" setup>
    const possibleSizes =[ "XS","S","L","XL","XXL"]


    const props =defineProps(
        {
            selectedSize:{
                type:String,
                required:true
            }
            
        }
    )

    const emits=defineEmits({
        onchangeSize:String
    })
</script>


<template>
    <div>
        {{selectedSize}}
        <button v-for="size in possibleSizes" :class="{'active':props.selectedSize===size}" @click="emits('onchangeSize',size)" >
        
                    {{size}}
        </button>        
    </div>
</template>

