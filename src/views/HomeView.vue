<template>
  <div>
    <h1>Harga Bitcoin Hari Ini</h1>
    <table>
      <thead>
        <tr>
          <th>Mata Uang</th>
          <th>Harga Jual</th>
          <th>Harga Beli</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(rate, currency) in rates" :key="currency">
          <td>{{ currency }}</td>
          <td>{{ rate.buy }}</td>
          <td>{{ rate.sell }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      rates: {},
    };
  },
  created() {
    this.fetchBitcoinRates();
  },
  methods: {
    fetchBitcoinRates() {
      axios.get('https://blockchain.info/ticker')
        .then(response => {
          this.rates = response.data;
        })
        .catch(error => {
          console.error(error);
        });
    },
  },
};
</script>