<template>
  <div class="min-h-screen flex flex-col justify-between">
    <div class="sm:w-10/12 md:w-1/2 lg:w-1/3 my-4 mx-auto relative">
      <h1 class="text-center text-xl font-semibold">
        Crypto Trading Profit Calculator.
      </h1>
      <div class="p-4 mt-4 flex flex-col justify-around">
        <div>
          <label for="amount">Amount</label>
          <input
            type="number"
            class="
              px-2
              py-1.5
              rounded
              border border-gray-700
              bg-gray-800
              focus:shadow
              w-full
            "
            v-model.number="amount"
            id="amount"
          />
        </div>
        <div>
          <label for="buy">Buy Price</label>
          <input
            type="number"
            class="
              px-2
              py-1.5
              rounded
              border border-gray-700
              bg-gray-800
              focus:shadow
              w-full
            "
            v-model.number="buy"
            id="buy"
          />
        </div>
        <div>
          <label for="sell">Sell Price</label>
          <input
            type="number"
            class="
              px-2
              py-1.5
              rounded
              border border-gray-700
              bg-gray-800
              focus:shadow
              w-full
            "
            v-model.number="sell"
            id="sell"
          />
        </div>
        <div>
          <label for="fees">Fees(%)</label>
          <input
            type="number"
            class="
              px-2
              py-1.5
              rounded
              border border-gray-700
              bg-gray-800
              focus:shadow
              w-full
            "
            v-model.number="fees"
            id="fees"
          />
        </div>
        <div>
          <label for="profit">Profit</label>
          <input
            type="number"
            class="
              px-2
              py-1.5
              rounded
              border border-gray-700
              bg-gray-700
              text-gray-400
              focus:shadow
              w-full
            "
            disabled
            v-model.number="profit"
            id="profit"
          />
        </div>
        <div>
          <button
            class="
              bg-blue-500
              text-white
              rounded
              focus:shadow-sm
              focus:bg-blue-400
              px-2
              py-1.5
              w-full
              mt-3
            "
            @click="calcProfit()"
          >
            Calculate
          </button>
        </div>
      </div>
      <div class="rounded p-2 m-2 border border-gray-800" v-show="profit">
        <p>
          Coins: <span class="text-blue-400">{{ calcHaving() }}</span>
          <br />
          Earn: <span class="text-green-400">${{ calcEarn() }}</span>
          <br />
          Profit Percentage:
          <span class="text-purple-300">{{ percentage }}%</span>
          <br />
           Total fees: <span class="text-gray-200">${{ calcFees() }}</span>
        </p>
      </div>
    </div>
    <Footer />
  </div>
</template>
<script>
import Footer from './Footer.vue'
export default {
  components: {
    Footer,
  },
  data() {
    return {
      amount: 1000,
      buy: 100,
      sell: 200,
      having: null,
      earn: null,
      profit: null,
      percentage: null,
      fees: 0.1,
    }
  },
  methods: {
    calcProfit: function () {
      this.profit = this.calcEarn() - this.amount - this.calcFees()
    },
    fixedNumber: function (val, n = 2) {
      return Number(val).toFixed(n)
    },
    calcFees: function () {
      return this.fixedNumber((this.amount / 100) * this.fees)
    },
    calcHaving: function () {
      return this.amount / this.buy
    },
    calcEarn: function () {
      return this.calcHaving() * this.sell
    },
    calcPercentage: function () {
      this.percentage = this.fixedNumber((this.profit / this.amount) * 100)
    },
  },
  watch: {
    amount: function () {
      this.calcProfit()
    },
    having: function () {
      this.calcEarn()
    },
    earn: function () {
      this.calcProfit()
    },
    buy: function () {
      this.calcHaving()
      this.calcProfit()
    },
    sell: function () {
      this.calcEarn()
      this.calcProfit()
    },
    fees: function () {
      this.calcFees()
      this.calcProfit()
    },
    profit: function () {
      this.calcFees()
      this.calcPercentage()
    },
  },
}
</script>