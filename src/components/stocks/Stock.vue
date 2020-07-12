<template>
  <v-col cols="12" xs="12" md="6" lg="4">
    <v-card tile class="green darken-3 white--text">
      <v-card-title class="headline">
        <strong>{{ stock.name }} <small>(Price: {{ stock.price | currency }})</small></strong>
      </v-card-title>
    </v-card>
    <v-card tile>
      <v-container fill-height>
        <v-text-field
          label="Quantity"
          type="number"
          class="mr-3"
          v-model.number="quantity"
          :error="insuficientFunds || !Number.isInteger(quantity)"/>
        <v-btn
          tile
          class="green darken-3 white--text"
          @click="buyStock"
          :disabled="quantity <= 0 || !Number.isInteger(quantity) || insuficientFunds"
        >
          {{ insuficientFunds ? 'Insuficient Funds' : 'Buy' }}
        </v-btn>
      </v-container>
    </v-card>
  </v-col>
</template>

<script>
import { mapActions } from 'vuex'

export default {
  props: {
    stock: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      quantity: 0
    }
  },
  computed: {
    funds() {
      return this.$store.getters.funds
    },
    insuficientFunds() {
      return this.quantity * this.stock.price > this.funds
    }
  },
  methods: {
    ...mapActions({
      buyStockAction: 'buyStock'
    }),
    buyStock() {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity
      }
      this.buyStockAction(order)
      this.quantity = 0
    }
  }
}
</script>

<style>

</style>