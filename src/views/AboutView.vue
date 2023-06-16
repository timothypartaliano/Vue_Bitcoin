<template>
  <div>
    <h1>Konversi Rupiah ke Bitcoin</h1>
    <div v-if="loading">Loading...</div>
    <div v-else>
      <p>1 BTC = {{ btcPrice }} USD</p>
      <label>Rupiah:</label>
      <input type="number" v-model="rupiahAmount">
      <button @click="convertToBitcoin">Convert</button>
      <p v-if="bitcoinAmount">Bitcoin: {{ bitcoinAmount }} BTC</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      btcPrice: null,
      rupiahAmount: null,
      bitcoinAmount: null,
      loading: true,
    };
  },
  mounted() {
    this.fetchBitcoinPrice();
  },
  methods: {
    fetchBitcoinPrice() {
      fetch('https://blockchain.info/ticker')
        .then(response => response.json())
        .then(data => {
          this.btcPrice = data.USD.last;
          this.loading = false;
        })
        .catch(error => {
          console.error('Error:', error);
          this.loading = false;
        });
    },
    convertToBitcoin() {
      if (this.rupiahAmount) {
        const usdAmount = this.rupiahAmount / 14000;
        this.bitcoinAmount = (usdAmount / this.btcPrice).toFixed(8);
      }
    },
  },
};
</script>

