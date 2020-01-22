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
        <div class="mb-4">{{ count }} {{ count | getWordItem }}</div>
        <ul>
          <li
            v-for="product in products"
            v-if="isCorrectCategory(product.category) && isCorrectBrand(product.brand)"
          >
            <nuxt-link :to="`/${product.id}`">
              {{ product.name }}, {{ product.category }}, {{ product.brand }}
            </nuxt-link>
          </li>
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
        products: this.$store.state.products,
        count: 0
      }
    },
    methods: {
      isCorrectCategory (category) {
        if (this.selectCategory.length === 0) {
          return  true
        } else if (this.selectCategory.includes(category)) {
          return  true
        } else {
          return false
        }
      },
      isCorrectBrand (brand) {
        if (this.selectBrand.length === 0) {
          return  true
        } else if (this.selectBrand.includes(brand)) {
          return  true
        } else {
          return false
        }
      },
      changeCount () {
        this.products.forEach((item) => {
          if (this.isCorrectCategory(item.category) && this.isCorrectBrand(item.brand)) {
            ++this.count
          }
        })
      }
    },
    watch: {
      selectCategory () {
        this.count = 0
        this.changeCount()
      },
      selectBrand () {
        this.count = 0
        this.changeCount()
      },
    },
     created() {
       this.changeCount()
     }
  }
</script>
