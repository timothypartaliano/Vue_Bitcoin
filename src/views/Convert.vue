<template>
    <div>
      <h1>Konversi Bitcoin ke Rupiah</h1>
      <div>
        <label>Bitcoin:</label>
        <input type="number" v-model="bitcoinAmount" step="0.0001" min="0">
      </div>
      <div>
        <label>Rupiah:</label>
        <input type="text" v-model="rupiahAmount" readonly>
      </div>
      <button @click="convertBitcoinToRupiah">Convert</button>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        bitcoinAmount: 0,
        rupiahAmount: 0
      }
    },
    methods: {
      convertBitcoinToRupiah() {
        const url = 'https://blockchain.info/tobtc?currency=USD&value=1';
        fetch(url)
          .then(response => response.json())
          .then(data => {
            const bitcoinRate = data;
            const rupiahRate = bitcoinRate * 14000;
            this.rupiahAmount = (this.bitcoinAmount * rupiahRate).toFixed(2);
          })
          .catch(error => {
            console.error('Error:', error);
          });
      }
    }
  }
  </script>
  