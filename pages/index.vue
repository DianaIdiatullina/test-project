<template>
  <v-container fluid>
    <v-row align="center">
      <v-col cols="12" sm="6">
        <v-subheader>Category</v-subheader>
      </v-col>
      <v-col cols="12" sm="6">
        <v-select
          v-model="selectCategory"
          :items="products"
          item-text="category"
          item-value="category"
          label="Select category"
          chips
          multiple
        ></v-select>
      </v-col>

      <v-col cols="12" sm="6">
        <v-subheader>Brand</v-subheader>
      </v-col>
      <v-col cols="12" sm="6">
        <v-select
          v-model="selectBrand"
          :items="products"
          item-text="brand"
          item-value="brand"
          label="Select brand"
          chips
          multiple
        ></v-select>
      </v-col>

      <v-col cols="12" sm="6">
        <ul v-if="selectCategory.length > 0 || selectBrand.length > 0">
          <li
            v-for="product in products"
            v-if="selectCategory.includes(product.category) || selectBrand.includes(product.brand)"
          >{{ product.name }}</li>
        </ul>
        <ul v-if="selectCategory.length === 0 && selectBrand.length === 0">
          <li
            v-for="product in products"
          >{{ product.name }}</li>
        </ul>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  export default {
    data () {
      return {
        selectCategory: [],
        selectBrand: [],
        products: this.$store.state.products
      }
    },
    // created() {
    //   console.log(this.selectCategory)
    //   console.log(this.selectBrand)
    // }
  }
</script>
