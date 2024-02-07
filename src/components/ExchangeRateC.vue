<template>
    <section>
      <h2>Exchange rates for Table C</h2>
      <p id="currentExchangeDateParagraphC">{{ exchangeRateDateText }}</p>
      <table id="currencyExchangeRatesTableC">
        <thead>
          <tr>
            <th>Currency</th>
            <th>Code</th>
            <th>Bid Rate</th>
            <th>Ask Rate</th>
          </tr>
        </thead>
        <tbody>

        </tbody>
      </table>
      <form @submit.prevent="showBidAskExchangeRates" id="currencyExchangeRateC">
        <button class="boldTextButton" type="submit">Show Bid-Ask Exchange Rates</button>
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
      showBidAskExchangeRates() {
        fetch('http://api.nbp.pl/api/exchangerates/tables/C/')
          .then(response => {
            if (!response.ok) {
              throw new Error(`HTTP error! Status: ${response.status}`);
            }
            return response.json();
          })
          .then(data => {
            const tableCdata = data[0];
            const { effectiveDate: tableCDate, rates: exchangeCRates } = tableCdata;
  
            this.exchangeRateDateText = `On the ${tableCDate} the exchange rates are:`;
            this.exchangeRatesData = exchangeCRates;
          })
          .catch(error => {
            console.error('Error fetching data:', error);
            this.exchangeRateDateText = 'There has been an error when fetching data.';
          });
      }
    },
    watch: {
      exchangeRatesData(newData) {
        const tableBody = this.$el.querySelector('#currencyExchangeRatesTableC tbody');
  
        while (tableBody.rows.length > 0) {
          tableBody.deleteRow(0);
        }
  
        newData.forEach(exchangeCRatesData => {
          const { currency: currencyName, code: currencyCode, bid: bidExchangeRate, ask: askExchangeRate } = exchangeCRatesData;
          const newRow = tableBody.insertRow(-1);
  
          const cell1 = newRow.insertCell(0);
          const cell2 = newRow.insertCell(1);
          const cell3 = newRow.insertCell(2);
          const cell4 = newRow.insertCell(3);
  
          cell1.textContent = currencyName;
          cell2.textContent = currencyCode;
          cell3.textContent = bidExchangeRate;
          cell4.textContent = askExchangeRate;
        });
      }
    }
  };
  </script>
  
  <style>

  </style>
  