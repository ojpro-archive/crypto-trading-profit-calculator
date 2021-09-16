<template>
  <div class="min-h-screen flex flex-col justify-between">
    <div class="sm:w-10/12 md:w-1/2 lg:w-1/3 my-4 mx-auto relative">
      <h1 class="text-center text-xl font-semibold">
        Trading Profit Calculator.
      </h1>
      <div class="p-4 mt-4 flex flex-col justify-around">
        <label for="amount">Amount</label>
        <Input v-model="amount" inputName="amount" />
        <label for="buy">buy</label>
        <Input v-model="buy" inputName="buy" />
        <label for="sell">sell</label>
        <Input v-model="sell" inputName="sell" />
        <label for="fees">Fees</label>
        <Input v-model="fees" inputName="fees" />
        <label for="profit">Profit</label>
        <Input v-model="profit" inputName="profit" />
        <div>
          <Button name="Calculate" @click="calcProfit()" />
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
import Input from '../components/Input.vue'
import Button from '../components/Button.vue'
export default {
  components: {
    Footer,
    Input,
    Button,
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