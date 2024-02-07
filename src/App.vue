<script setup>

import CurrentGoldPrice from '@/components/showCurrentGoldPrice.vue';
import ExchangeRateC from '@/components/ExchangeRateC.vue';
import ExchangeRateA from '@/components/ExchangeRateA.vue';
import ExchangeRateB from '@/components/ExchangeRateB.vue';
</script>

<template>
  <div>
    <h1>NBP Web API</h1>
    <CurrentGoldPrice />
    <ExchangeRateC />
    <ExchangeRateA />
    <ExchangeRateB />
  </div>
</template>

<style>
body {
  color: rgb(129, 135, 44);
  font-size: 11px;
  font-weight:900;
}

h1 {
  margin: 20px 0 0 30px;
  font-weight: 900;
}
  
section {
  margin: 20px;
  padding: 10px;
  border: 2px solid #fff;
  border-radius: 5px;
  background-color: #f0f0f0;
}

section h2 {
  font-weight:900;
}

h2 {
  margin-bottom: 10px;
  color: #333;
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
  font-weight: 900;
}

.boldTextButton {
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  font-size: 15px;
  font-weight: 700;
  background-color: rgb(215, 232, 232);
  border-radius: 10px;
  margin-top: 10px;
  padding: 5px;
  box-shadow: #333;
}
</style>
