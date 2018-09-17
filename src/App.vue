<template>
  <div id="app">
    <h1>Bitcoin Price Index</h1>
    <li 
      v-for="currency in info"
      v-bind:key="currency.rate">
        {{ currency.description }}
        <span>
          <span v-html="currency.symbol"></span>
         {{ currency.rate_float | currencydecimal }}
        </span>
    </li>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      info: null
    };
  },
  filters: {
    currencydecimal(value){
      return value.toFixed(2)    
    }
  },
  mounted(){
    axios.get('https://api.coindesk.com/v1/bpi/currentprice.json')
    .then((response) => {
      this.info = response.data.bpi;
      console.log(this.info)
    })
  }
};

</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
