<script setup lang="ts">

import CriptoVue from './Cripto.vue';
import FiatVue from './Fiat.vue';
import { ref, onMounted,reactive} from 'vue'
import axios from 'axios'

type InputDefaultCalculatorExchangeType = 'fiat' | 'crypto'
type StatesCalulatorType = 'loading' | 'success' | 'error'
export type FiatCurrencyType = 'PEN' | 'USD'

// type CryptoCurrencyType = 'USDT'

export interface CalculatorExchangeProps {
  inputDefault?: InputDefaultCalculatorExchangeType
}

withDefaults(defineProps<CalculatorExchangeProps>(), {
  inputDefault: 'fiat',
})

let state = ref<StatesCalulatorType>('loading')
// let orderInputs = ref(true)
// let fiatAmount = ref(0)
// let fiatCurrency = ref<FiatCurrencyType>('PEN')
// let cryptoAmount = ref(0)
// let cryptoCurrency = ref<CryptoCurrencyType>('USDT')
// let lastInputEdited = ref(null)
let currentDate = ref('')
let interval = ref<Timer>()
let time = ref('')
let params = ref({})

const currencySelected = ref('')
const btnColorPEN = ref()
const btnColorUSD = ref()

onMounted(() => {
  setup()
  getParams()
  loadTimer()

  // AGREGANDO GET PARANMS



})

function setup() {
  currencySelected.value = 'PEN'
  updateCurrencySelected()
}

function getParams() {
  state.value = 'loading'
  // let urlAPI = import.meta.env.VITE_APP_API
  let urlAPI="https://criptobank.pe/api"

  axios
    .get( urlAPI + '/params')
    .then((response) => {
      state.value = 'success'
      params = response.data
      PENSD.value=params.value.tc.penusd
    })
    .catch((error) => {
      state.value = 'error'
      if (!error.response) {
        console.log(error)
      } else {
        console.log(error.response.data.message)
      }
    })
}

function loadTimer() {
  const today = new Date()
  const monthNames = [
    'Enero',
    'Febrero',
    'Marzp',
    'Abril',
    'Mayo',
    'Junio',
    'Julio',
    'Agoto',
    'Setiembre',
    'Octubre',
    'Nov',
    'Diciembre',
  ]
  let weekdays = [
    'Domingo',
    'Lunes',
    'Martes',
    'Miercoles',
    'Jueves',
    'Viernes',
    'Sábado',
  ]
 
  currentDate.value =
    weekdays[today.getDay()] +
    ', ' +
    today.getDate() +
    ' ' +
    monthNames[today.getMonth()]
  interval.value = setInterval(() => {
    time.value = Intl.DateTimeFormat(navigator.language, {
      hour: 'numeric',
      minute: 'numeric',
      second: 'numeric',
    }).format()
  }, 1000)
}

function updateCurrencySelected() {
  if (currencySelected.value === 'PEN') {
    btnColorPEN.value = 'primary'
    btnColorUSD.value = null
  } else {
    btnColorPEN.value = null
    btnColorUSD.value = 'primary'
  }
}

function setCurrencySelected(currency: FiatCurrencyType) {
  currencySelected.value = currency
  updateCurrencySelected()
}
// valores
const fiatAmount = ref(0)
const criptoAmount=ref(0)
const PENSD=ref("")
const fiatCurrency=ref("PEN")
 const modificarValor=(k)=>{
        fiatAmount.value=k
        console.log(PENSD.value)
        console.log(PENSD.value)

    }
// cambio 
 
  // const updateCryptoAmountFromFiat=(fiatAmount = 0) =>{
  //           let totalUSDT = 0
  //           let amount = fiatAmount === 0 ? fiatAmount.value : fiatAmount
  //           let fiatCharge = params.fiatCharge.find(fiat => fiat.code === fiatCurrency.value)
  //           let charge = 1 + (fiatCharge.chargePercentage / 100)

  //           switch (fiatCurrency.value) {
  //               case 'PEN':
  //                   totalUSDT = amount / PENSD.value/ charge
  //                   break

  //               case 'USD':
  //                   totalUSDT = amount / charge
  //                   break

  //               default:
  //                   break
  //           }

  //           let cryptoCharge = params.cryptoCharge.find(crypto => crypto.code === cryptoCurrency.value)

  //           cryptoAmount.value = (totalUSDT - cryptoCharge.charge).toFixed(1) + '0'
  //       }


</script>

<template>
  <div>
    <div class="exchange">
      <div class="timerlive">
        <small>{{ currentDate }} {{ time }}</small>
      </div>
      <h5 class="ex-head">
        Fiat
        <br />
        Exchange
      </h5>
      <div>
        <div class="has-text-right">
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
        </div>

  
            <!-- <VInput rounded size="lg" /> -->
              <FiatVue :valor="fiatAmount" v-on:modificarValor="modificarValor" />
        

       
            <!-- <VInput rounded size="lg" /> -->
                 <CriptoVue :valor="criptoAmount" v-on:modificarValor="modificarValor"/>

  
        
      </div>
      <Button class="mt-4" color="primary" to="/register">Comprar</Button>
    </div>
  </div>
</template>
