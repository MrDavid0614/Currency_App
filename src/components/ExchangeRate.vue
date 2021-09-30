<template>
  <li v-if="currentCurrency !== currencyRate.name">
      {{ currencyRate.name }} : {{ currencyRate.value }}
  </li>
</template>

<script>
export default {
    props: {
        currentCurrency: {
            type: String,
            required: true,
        },
        currencyRate: {
            type: Object,
            required: true
        }
    }
}
</script>

<style>

</style>