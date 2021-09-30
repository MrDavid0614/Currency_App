<template>
  <div class="exchanges-container">
      <span v-if="isLoading">Loading...</span>
      <ol v-else>
          <ExchangeRate 
            v-for="(currencyRate, index) in currencyRates"
            :key="index"
            :currentCurrency="currentCurrency"
            :currencyRate="currencyRate" 
            />
      </ol>
  </div>
</template>

<script>
import ExchangeRate from "./ExchangeRate.vue"

export default {
    props: {
        isLoading: {
            type: Boolean,
            required: true
        },
        currentCurrency: {
            type: String,
            required: true
        },
        currencyRates: {
            type: Array,
            required: true
        }
    },
    components: {
        ExchangeRate
    }
}
</script>

<style>
.exchanges-container {
    display: flex;
    justify-content: center;
}
</style>