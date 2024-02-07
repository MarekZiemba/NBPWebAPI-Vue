<template>
  <section>
    <h2>Current Gold Price</h2>
    <p id="currentGoldPriceParagraph">On the 
      <span class="goldDate"> {{ goldDate }} </span> 
      the price is 
      <span class="goldPrice"> {{ goldPrice }} </span>
      PLN/g.
    </p>
    <form @submit.prevent="showCurrentGoldPrice" id="currentGoldPriceForm">
      <button class="boldTextButton" type="submit">Show Current Gold Price</button>
    </form>
  </section>
</template>

<script>
export default {
  data() {
    return {
      goldDate: '',
      goldPrice: ''
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
          this.goldDate = goldDate;
          this.goldPrice = goldPrice;
        })
        .catch(error => {
          console.error('Error fetching data:', error);
          this.goldDate = '';
          this.goldPrice = 'There has been an error when fetching data.';
        });
    }
  }
};
</script>

<style>
#currentGoldPriceParagraph {
  color: #3d3d3d;
  font-weight: 700;
}

.goldDate {
  color: #4CAF50;
  font-weight: 800;
}

.goldPrice {
  color: #d8c703;
  font-weight: 900;
}


</style>
