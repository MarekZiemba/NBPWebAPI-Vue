<template>
    <section>
      <h2>Average exchange rates for Table B</h2>
      <p id="currentExchangeDateParagraphB">{{ exchangeRateDateText }}</p>
      <table id="currencyExchangeRatesTableB">
        <thead>
          <tr>
            <th>Currency</th>
            <th>Code</th>
            <th>Mid Rate</th>
          </tr>
        </thead>
        <tbody>

        </tbody>
      </table>
      <form @submit.prevent="showMidExchangeRatesB" id="currencyExchangeRateB">
        <button class="boldTextButton" type="submit">Show Mid Exchange Rates</button>
      </form>
    </section>
  </template>
  
  <script>
  export default {
    data() {
      return {
        exchangeRateDateText: '',
        exchangeRatesData: []
      };
    },
    methods: {
      showMidExchangeRatesB() {
        fetch('http://api.nbp.pl/api/exchangerates/tables/B/')
          .then(response => {
            if (!response.ok) {
              throw new Error(`HTTP error! Status: ${response.status}`);
            }
            return response.json();
          })
          .then(data => {
            const tableBdata = data[0];
            const { effectiveDate: tableBDate, rates: exchangeBRates } = tableBdata;
  
            this.exchangeRateDateText = `On the ${tableBDate} the exchange rates are:`;
            this.exchangeRatesData = exchangeBRates;
          })
          .catch(error => {
            console.error('Error fetching data:', error);
            this.exchangeRateDateText = 'There has been an error when fetching data.';
          });
      }
    },
    watch: {
      exchangeRatesData(newData) {
        const tableBody = this.$el.querySelector('#currencyExchangeRatesTableB tbody');
  
        while (tableBody.rows.length > 0) {
          tableBody.deleteRow(0);
        }
  
        newData.forEach(exchangeBRatesData => {
          const { currency: currencyName, code: currencyCode, mid: midExchangeRate } = exchangeBRatesData;
          const newRow = tableBody.insertRow(-1);
  
          const cell1 = newRow.insertCell(0);
          const cell2 = newRow.insertCell(1);
          const cell3 = newRow.insertCell(2);
  
          cell1.textContent = currencyName;
          cell2.textContent = currencyCode;
          cell3.textContent = midExchangeRate;
        });
      }
    }
  };
  </script>
  
  <style>

  </style>
  