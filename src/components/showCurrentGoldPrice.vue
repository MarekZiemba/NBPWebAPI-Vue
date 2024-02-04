<template>
    <section>
      <h2>Current Gold Price</h2>
      <p id="currentGoldPriceParagraph">{{ goldPriceText }}</p>
      <form @submit.prevent="showCurrentGoldPrice" id="currentGoldPriceForm">
          <button type="submit">Show Current Gold Price</button>
      </form>
    </section>
  </template>
  
  <script>
  export default {
    data() {
      return {
        goldPriceText: ''
      };
    },
    methods: {
      showCurrentGoldPrice() {
        fetch('http://api.nbp.pl/api/cenyzlota')
          .then(response => {
            if (!response.ok) {
              throw new Error(`HTTP error! Status: ${response.status}`);
            }
            return response.json();
          })
          .then(data => {
            const goldData = data[0];
            const { data: goldDate, cena: goldPrice } = goldData;
            this.goldPriceText = `On the ${goldDate} the price is ${goldPrice} PLN/g.`;
          })
          .catch(error => {
            console.error('Error fetching data:', error);
            this.goldPriceText = 'There has been an error when fetching data.';
          });
      }
    }
  };
  </script>
  
  <style>

  </style>
  