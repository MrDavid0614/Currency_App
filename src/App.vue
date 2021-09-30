<template>
<!-- EUR, USD, BRL, PEN, and ARS -->
  <section class="container">
    <select v-model="currentCurrency">
      <option 
        v-for="(currency, index) in currencies"
        :key="index"
      >{{ currency }}</option>
    </select>

    <ExchangeRates
      :isLoading="isLoading"
      :currentCurrency="currentCurrency" 
      :currencyRates="currencyRates" 
    />
  </section>
</template>

<script>
import axios from 'axios';
import ExchangeRates from './components/ExchangeRates.vue'

export default {
  name: 'App',
  created () {
    this.fetchCurrencyRates(this.currentCurrency)
  },
  data () {
    return {
      currencies: ['USD', 'EUR', 'BRL', 'PEN', 'ARS'],
      currentCurrency: 'USD',
      currencyRates: [],
      isLoading: true,
    }
  },
  watch: {
    currentCurrency(newCurrency) {
      this.fetchCurrencyRates(newCurrency)
    }
  },
  methods: {
    fetchCurrencyRates (currency) {
      this.isLoading = true;

      const apiURL = `https://v6.exchangerate-api.com/v6/72179b357c84d84fcb2c1f3d/latest/${ currency }`;

      axios.get(apiURL)
        .then(({ data }) => {
          const filteredCurrencies = this.currencies.filter(currency => currency in data.conversion_rates)
                                                    .map(currency => ({
                                                      name: currency,
                                                      value: data.conversion_rates[currency]
                                                    }));
          this.currencyRates = filteredCurrencies
          this.isLoading = false;
        })
        .catch(() => {
          this.isLoading = false;
          console.warn("Something wrong happened, please try later...")
        })
      
    }
  },
  components: {
    ExchangeRates
  }
}
</script>

<style>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
