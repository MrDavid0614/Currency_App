<template>
  <div class="exchanges-container">
      <ol v-if="currencyRates.length">
          <li 
            v-for="(currencyRate, index) in currencyRates"
            v-show="currentCurrency !== currencyRate.name"
            :key="index"
            >
                <span>{{ currencyRate.name }} : {{ currencyRate.value }}</span>
            </li>
      </ol>
  </div>
</template>

<script>
export default {
    props: {
        currentCurrency: {
            type: String,
            required: true
        },
        currencyRates: {
            type: Array,
            required: true
        }
    }
}
</script>

<style>
.exchanges-container {
    display: flex;
    justify-content: center;
}
</style>