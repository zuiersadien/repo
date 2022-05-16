<script setup lang="ts">

import CriptoVue from './Cripto.vue';
import FiatVue from './Fiat.vue';
import { ref, onMounted,provide} from 'vue'
import axios from 'axios'

// type InputDefaultCalculatorExchangeType = 'fiat' | 'crypto'
// type StatesCalulatorType = 'loading' | 'success' | 'error'
// export type FiatCurrencyType = 'PEN' | 'USD'

// // type CryptoCurrencyType = 'USDT'

// export interface CalculatorExchangeProps {
//   inputDefault?: InputDefaultCalculatorExchangeType
// }

// withDefaults(defineProps<CalculatorExchangeProps>(), {
//   inputDefault: 'fiat',
// })

// let state = ref<StatesCalulatorType>('loading')
// // let orderInputs = ref(true)
// // let fiatAmount = ref(0)
// // let fiatCurrency = ref<FiatCurrencyType>('PEN')
// // let cryptoAmount = ref(0)
// // let cryptoCurrency = ref<CryptoCurrencyType>('USDT')
// // let lastInputEdited = ref(null)
// let currentDate = ref('')
// let interval = ref<Timer>()
// let time = ref('')
// let params = ref({})

// const currencySelected = ref('')
// const btnColorPEN = ref()
// const btnColorUSD = ref()

// onMounted(() => {
//   setup()
//   getParams()
//   loadTimer()
// })

// function setup() {
//   currencySelected.value = 'PEN'
//   updateCurrencySelected()
// }

// function getParams() {
//   state.value = 'loading'
//   let urlAPI = import.meta.env.VITE_APP_API

//   axios
//     .get(urlAPI + '/params')
//     .then((response) => {
//       state.value = 'success'
//       params.value = response.data
//     })
//     .catch((error) => {
//       state.value = 'error'
//       if (!error.response) {
//         console.log(error)
//       } else {
//         console.log(error.response.data.message)
//       }
//     })
// }

// function loadTimer() {
//   const today = new Date()
//   const monthNames = [
//     'Enero',
//     'Febrero',
//     'Marzp',
//     'Abril',
//     'Mayo',
//     'Junio',
//     'Julio',
//     'Agoto',
//     'Setiembre',
//     'Octubre',
//     'Nov',
//     'Diciembre',
//   ]
//   let weekdays = [
//     'Domingo',
//     'Lunes',
//     'Martes',
//     'Miercoles',
//     'Jueves',
//     'Viernes',
//     'Sábado',
//   ]
 
//   currentDate.value =
//     weekdays[today.getDay()] +
//     ', ' +
//     today.getDate() +
//     ' ' +
//     monthNames[today.getMonth()]
//   interval.value = setInterval(() => {
//     time.value = Intl.DateTimeFormat(navigator.language, {
//       hour: 'numeric',
//       minute: 'numeric',
//       second: 'numeric',
//     }).format()
//   }, 1000)
// }

// function updateCurrencySelected() {
//   if (currencySelected.value === 'PEN') {
//     btnColorPEN.value = 'primary'
//     btnColorUSD.value = null
//   } else {
//     btnColorPEN.value = null
//     btnColorUSD.value = 'primary'
//   }
// }

// function setCurrencySelected(currency: FiatCurrencyType) {
//   currencySelected.value = currency
//   updateCurrencySelected()
// }
// 

  


const valor = ref(0)

 const modificarValor=(k)=>{
        valor.value=k
    }
// 


</script>

<template>
  <div>
    <div class="exchange">
      <div class="timerlive">
        <!-- <small>{{ currentDate }} {{ time }}</small> -->
      </div>
      <h5 class="ex-head">
        Fiat
        <br />
        Exchange
      </h5>
      <div>
        <!-- <div class="has-text-right">
          <Button
            size="small"
            :color="btnColorPEN"
            @click="setCurrencySelected('PEN')"
          >
            Soles
          </Button>
          <Button
            size="small"
            :color="btnColorUSD"
            @click="setCurrencySelected('USD')"
          >
            Dolares
          </Button>
        </div> -->

        <Field>
          <FieldLabel type="hero" label="Tu nos envías"></FieldLabel>
          <Control>
            <VInput rounded size="lg" />
          </Control>
        </Field>

        <Field>
          <FieldLabel type="hero" label="Recibirás"></FieldLabel>
          <Control>
            <VInput rounded size="lg" />
          </Control>
        </Field>
        <CriptoVue :valor="valor" v-on:modificarValor="modificarValor"/>
        <FiatVue :valor="valor" v-on:modificarValor="modificarValor" />
      </div>
      <Button class="mt-4" color="primary" to="/register">Comprar</Button>
    </div>
  </div>
</template>
