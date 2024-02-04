<script setup>

import CurrentGoldPrice from '@/components/showCurrentGoldPrice.vue';
import ExchangeRateC from '@/components/ExchangeRateC.vue';
import ExchangeRateA from '@/components/ExchangeRateA.vue';
import ExchangeRateB from '@/components/ExchangeRateB.vue';
</script>

<template>
  <div>
    <CurrentGoldPrice />
    <ExchangeRateC />
    <ExchangeRateA />
    <ExchangeRateB />
  </div>
</template>

<style>
section {
  margin: 20px;
  border: 2px solid #fff;
  border-radius: 5px;
}
.pagination {
  list-style: none;
  display: flex;
}

.pagination li {
  cursor: pointer;
}

.pagination li:hover {
  color: #fff;
}

.pagination li.active {
  color: #fff;
  font-weight: bold;
}
</style>
