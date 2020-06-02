<template>
  <!-- v-bind:key="crypto" -->
  <div class="hello">
    <div>
      <div id="container" v-for="(crypto, key) in cryptos" v-bind:key="crypto">
        <span class="left">{{ key }}</span>
        <span class="right">${{ crypto.USD }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "hello",
  data: () => ({
    cryptos: [],
    errors: []
  }),
  created() {
    axios
      .get(
        "https://min-api.cryptocompare.com/data/pricemulti?fsyms=BTC,ETH,DAI&tsyms=USD"
      )
      .then(response => {
        console.log("RESP", response);
        this.cryptos = response.data;
      })
      .catch(e => {
        this.errors.push(e);
      });
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
body {
  background: #f1f1f1;
}

#container {
  background: white;
  width: 70%;
  margin: 0 auto 4px auto;
  padding: 2em;
  box-shadow: 0px 4px 4px lightgrey;
}

span.left {
  font-weight: bold;
}

span.right {
  float: right;
}
</style>
