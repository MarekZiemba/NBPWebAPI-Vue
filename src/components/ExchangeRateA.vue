<template>
    <section>
        <h2>Average exchange rates for Table A</h2>
        <p id="currentExchangeDateParagraphA">{{ exchangeRateDateText }}</p>
        <table id="currencyExchangeRatesTableA">
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
        <form @submit.prevent="showMidExchangeRatesA" id="currencyExchangeRateA">
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
        showMidExchangeRatesA() {
            fetch('http://api.nbp.pl/api/exchangerates/tables/A/')
                .then(response => {
                if (!response.ok) {
                    throw new Error(`HTTP error! Status: ${response.status}`);
                }
                return response.json();
                })
                .then(data => {
                const tableAdata = data[0];
                const { effectiveDate: tableADate, rates: exchangeARates } = tableAdata;

                this.exchangeRateDateText = `On the ${tableADate} the exchange rates are:`;
                this.exchangeRatesData = exchangeARates;
                })
                .catch(error => {
                console.error('Error fetching data:', error);
                this.exchangeRateDateText = 'There has been an error when fetching data.';
                });
        }
    },
    watch: {
        exchangeRatesData(newData) {
        const tableBody = this.$el.querySelector('#currencyExchangeRatesTableA tbody');

        while (tableBody.rows.length > 0) {
            tableBody.deleteRow(0);
        }

        newData.forEach(exchangeARatesData => {
            const { currency: currencyName, code: currencyCode, mid: midExchangeRate } = exchangeARatesData;
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
