<script>
/*
JAVASCRIPT PART
*/
export default {
  //Variablen global for component
  data() {
    return {
      display: '0',
      numbers: ['7', '8', '9', '4', '5', '6', '1', '2', '3', ','],
      operators: ['+', '-', '*', '/'],
    }
  },

  // functions / methods
  methods: {
    // method1
    addNumber(number) {
      console.log('test')
      if (this.display === '0') {
        this.display = number
      } else {
        this.display = this.display + number
      }
    },
    // Method n !

    factorial(n) {
      let result = 1

      for (let i = n; i >= 1; i--) {
        result = result * i
      }

      return result
    },
    // method2
    clearDisplay() {
      this.display = '0'
    },
    // method3
    addOperator(operator) {
      this.display = this.display + operator
    },
    // method4 calculate und ! n

    calculate() {
      if (this.display.includes('!')) {
        let number = this.display.replace('!', '')
        this.display = this.factorial(Number(number))
      } else {
        this.display = eval(this.display)
      }
    },
    // method +-*/!%
  },
  //lifecycle hooks (mounted, beforeMounted, beforeDestroy, ............................)
  mounted() {
    window.addEventListener('keydown', (event) => {
      if (!isNaN(event.key)) {
        this.addNumber(event.key)
      }
      if (['+', '-', '*', '/'].includes(event.key)) {
      this.addOperator(event.key)
    }
    if (event.key === 'Enter') {
      this.calculate()
    }
  })
  },
  // example: filtering a list live
  computed: {},
}
</script>

<template>
  <!-- NEU: Das "Paket", das alles in die Mitte schiebt -->
  <div class="min-h-screen w-full flex items-center justify-center bg-gray-100 p-4">
    
    <!-- Dein eigentlicher Taschenrechner bekommt jetzt einen schönen Rahmen -->
    <div class="bg-slate-800 p-6 rounded-3xl shadow-2xl border-4 border-slate-700">
      
      <h1 class="text-white text-center text-xl font-bold mb-4 uppercase tracking-widest">Taschenrechner</h1>
      
      <!-- Dein Display -->
      <div class="bg-white text-black text-right p-4 text-3xl rounded-xl mb-4 font-mono shadow-inner">
        {{ display }}
      </div>

      <div class="flex gap-4">
        <!--------------------------------------------------------->
        <!-- LINKS: Zahlen -->
        <div class="grid grid-cols-3 gap-2">
          <button
            v-for="num in numbers"
            :key="num"
            @click="addNumber(num)"
            class="rounded-lg bg-blue-500 px-6 py-4 text-white text-xl font-bold hover:bg-blue-600 shadow-md active:translate-y-1 transition-all"
          >
            {{ num }}
          </button>

          <button 
            @click="addNumber('0')" 
            class="col-span-2 rounded-lg bg-blue-500 px-6 py-4 text-white text-xl font-bold hover:bg-blue-600 shadow-md active:translate-y-1"
          >
            0
          </button>
        </div>

        <!--------------------------------------------------------->
        <!-- RECHTS: Operatoren -->
        <div class="flex flex-col gap-2">
          <button @click="addOperator('+')" class="rounded-lg bg-slate-600 px-5 py-3 text-white font-bold hover:bg-slate-500">+</button>
          <button @click="addOperator('-')" class="rounded-lg bg-slate-600 px-5 py-3 text-white font-bold hover:bg-slate-500">-</button>
          <button @click="addOperator('*')" class="rounded-lg bg-slate-600 px-5 py-3 text-white font-bold hover:bg-slate-500">*</button>
          <button @click="addOperator('/')" class="rounded-lg bg-slate-600 px-5 py-3 text-white font-bold hover:bg-slate-500">/</button>
          
          <button @click="clearDisplay()" class="rounded-lg bg-red-500 px-5 py-3 text-white font-bold hover:bg-red-600">C</button>
          <button @click="calculate()" class="rounded-lg bg-orange-500 px-5 py-3 text-white font-bold hover:bg-orange-600">=</button>
        </div>
      </div>

    </div> <!-- Ende des Rechners -->
  </div> <!-- Ende des Zentrier-Pakets -->
</template>

<style scoped></style>