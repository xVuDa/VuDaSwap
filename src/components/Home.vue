<template>
    <section class="section">
        <table class="table is-bordered is-striped is-narrow is-hoverable is-fullwidth">
            <thead>
                <tr class="is-selected">
                    <th>#</th>
                    <th>Moneda</th>
                    <th>Market Cap</th>
                    <th>Precio</th>
                    <th>Volumen (24h)</th>
                    <th>Monedas en circulacion</th>
                    <th>Precio hace 24h</th>
                </tr>
            </thead>
            <tfoot>
                <tr>
                    <th>#</th>
                    <th>Name</th>
                    <th>Market Cap</th>
                    <th>Price</th>
                    <th>Volume (24h)</th>
                    <th>Circulating Supply</th>
                    <th>Open (24h)</th>
                </tr>
            </tfoot>
            <tbody>
                <tr v-for="(value, key, index) in coins" v-bind:key="(value, key, index)">
                    <th>{{ index + 1 }}</th>
                    <td>{{ key }}</td>
                    <td>{{ value.EUR.MKTCAP }}</td>
                    <td>{{ value.EUR.PRICE }}</td>
                    <td>{{ value.EUR.VOLUME24HOUR }}</td>
                    <td>{{ value.EUR.SUPPLY }}</td>
                    <td>{{ value.EUR.OPEN24HOUR }}</td>
                </tr>
            </tbody>
        </table>
    </section>
</template>
<script>
import axios from 'axios'
export default {
  name: 'home',
  data: () => ({
    coins: [],
    errors: []
  }),
  created () {
//https://min-api.cryptocompare.com/data/pricemulti?fsyms=BTC,ETH,IOT&tsyms=USD
    //this.cryptos = response.data
      axios.get('https://min-api.cryptocompare.com/data/pricemultifull?fsyms=BTC,ETH,LUNA,ADA,MATIC,ROSE,DOT,NEXO,ANC&tsyms=USD,EUR')
      .then(response => {
       this.coins = response.data.DISPLAY
        console.log(response)
      })
      .catch(e => {
        this.errors.push(e)
      })
  }
}
</script>