<template>
  <v-col cols="12" xs="12" md="6" lg="4">
    <v-card tile class="blue darken-3 white--text">
      <v-card-title class="headline">
        <strong>{{ stock.name }} <small>(Price: {{ stock.price | currency }} | Qty: {{ stock.quantity }})</small></strong>
      </v-card-title>
    </v-card>
    <v-card tile>
      <v-container fill-height>
        <v-text-field
          label="Quantity"
          type="number"
          class="mr-3"
          v-model.number="quantity"
          :error="insufucientQuantity || !Number.isInteger(quantity)" />
        <v-btn
          tile
          class="blue darken-3 white--text"
          @click="sellStock"
          :disabled="quantity <= 0 || !Number.isInteger(quantity) || insufucientQuantity"
        >
          {{ insufucientQuantity ? 'Insuficient Quantity' : 'Sell' }}
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
    insufucientQuantity() {
      return this.quantity > this.stock.quantity
    }
  },
  methods: {
    ...mapActions({
      sellStockAction: 'sellStock'
    }),
    sellStock() {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity
      }
      this.sellStockAction(order)
      this.quantity = 0
    }
  }
}
</script>

<style>

</style>