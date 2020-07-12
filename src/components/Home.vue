<template>
  <div>
    <h1 class="text-h3 font-weight-light mt-2 mb-4">Trade and Check Out your Stocks</h1>
    <v-sheet elevation="3" class="pa-2 primary d-flex align-center">
      <v-icon dark class="mx-2">mdi-information</v-icon>
      <span class="headline font-weight-light white--text">
        You can Save &amp; Load your Data
      </span>
    </v-sheet>
    <v-sheet elevation="3" class="pa-2 mt-4 success darken-1 d-flex align-center">
      <v-icon dark class="mx-2">mdi-information</v-icon>
      <span class="headline font-weight-light white--text">
        Click on "End the Day" to start a new day
      </span>
    </v-sheet>
    <v-divider class="my-4"></v-divider>
    <p class="text-h5">
      <strong>Funds:</strong> {{ funds | currency }}
    </p>
  </div>
</template>

<script>
export default {
  computed: {
    funds() {
      return this.$store.getters.funds
    }
  }
}
</script>

<style>

</style>