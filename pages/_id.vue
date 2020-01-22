<template>
  <v-container fluid>
    <v-row align="center">
      <v-col cols="12" sm="6">
        <ul>
          <li>Name: {{ product.name }}</li>
          <li>Category: {{ product.category }}</li>
          <li>Brand: {{ product.brand }}</li>
        </ul>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  export default {
    data () {
      return {
        products: this.$store.state.products,
        product: {}
      }
    },
    created() {
      const url = +this.$route.params.id
      this.products.forEach((item) => {
        if (url === item.id) {
          this.product = item
        }
      })
    }
  }
</script>
