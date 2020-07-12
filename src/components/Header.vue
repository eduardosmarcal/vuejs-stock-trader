<template>
  <div>
    <v-app-bar>
      <v-toolbar-title class="headline text-uppercase mr-4">
        <span>Stock</span>
        <span class="font-weight-light">Trader</span>
      </v-toolbar-title>
      <v-toolbar-items>
        <v-btn text to="/">Home</v-btn>
        <v-btn text to="/portfolio">Portfolio</v-btn>
        <v-btn text to="/stocks">Stocks</v-btn>
      </v-toolbar-items>
      <v-spacer></v-spacer>
      <v-toolbar-items>
        <v-btn text @click="endDay">End the day</v-btn>
        <v-menu offsetY>
          <template v-slot:activator="{ on, attrs }">
            <v-btn
              v-bind="attrs"
              v-on="on"
              text
            >
              Save &amp; Load
            </v-btn>
          </template>
          <v-list>
            <v-list-item @click="save">
              <v-list-item-title>Save Data</v-list-item-title>
            </v-list-item>
            <v-list-item @click="load">
              <v-list-item-title>Load Data</v-list-item-title>
            </v-list-item>
          </v-list>
        </v-menu>
        <div class="d-flex align-center pl-4">
          <span class="text-uppercase text-button grey--text text--darken-2">
            Funds: {{ funds | currency }}
          </span>
        </div>
      </v-toolbar-items>
    </v-app-bar>
  </div>
</template>

<script>
import { mapActions } from 'vuex'

export default {
  computed: {
    funds() {
      return this.$store.getters.funds
    }
  },
  methods: {
    ...mapActions([
      'randomizeStocks',
      'loadData'
    ]),
    endDay() {
      this.randomizeStocks()
    },
    save() {
      const { funds, stockPortfolio, stocks } = this.$store.getters
      this.$http.put('data.json', { funds, stockPortfolio, stocks })
    },
    load() {
      this.loadData()
    }
  }
}
</script>

<style>

</style>