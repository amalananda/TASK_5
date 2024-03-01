<script>
// import SkeletonLoading from './SkeletonLoading.vue'

export default {
  // components: {
  //   SkeletonLoading
  // },
  props: {
    product: {
      type: Object,
      default: () => {
        return {
          title: '',
          rating: { rate: 0, count: 0 },
          image: '',
          category: '',
          price: '',
          description: ''
        }
      }
    },
    category: String,
    clickGetNextProduct: Function
  },
  data() {
    return {
      // product:
      loading: false,
      number: 0
      // category: ''
    }
  },

  methods: {
    // async getNextProduct() {
    //   this.loading = true
    //   try {
    //     if (this.number === 20) this.number = 0

    //     this.number = this.number + 1
    // Panggil API untuk mendapatkan produk berikutnya
    //     this.loading = true
    //     const response = await fetch(`https://fakestoreapi.com/products/${this.number}`)

    //     const data = await response.json()

    //     this.product = data

    //     switch (data.category) {
    //       case "men's clothing":
    //         this.category = 'men'
    //         break
    //       case "women's clothing":
    //         this.category = 'women'
    //         break
    //       default:
    //         this.category = 'nonGender'
    //     }
    //   } catch (error) {
    //     console.error('Error fetching product:', error)
    //   } finally {
    //     this.loading = false
    //   }
    // },
    getFilledColor(index) {
      let color

      // choose color base on category
      switch (this.product.category) {
        case "men's clothing":
          color = '#002772'
          break
        case "women's clothing":
          color = '#720060'
          break
        default:
          color = 'red'
      }

      const ceil_number = Math.ceil(this.product.rating.rate)

      // colored bullet by on rating number
      if (index <= ceil_number) {
        return color
      } else {
        return 'white' // Warna default atau tidak diisi
      }

      // Custom logic to determine the filled color based on the category
    },
    getNextProduct() {
      if (typeof this.clickGetNextProduct() === 'function') {
        this.clickGetNextProduct()
      }
    }
  }

  // mounted() {
  // Panggil metode untuk mendapatkan produk pertama saat komponen dimuat
  // this.getNextProduct()
  // }
}
</script>

<template>
  <!-- Product Card Component -->
  <div v-if="this.category == 'nonGender'">
    <img src="../assets/sad-face.png" />
  </div>
  <div v-else class="product-card">
    <div class="product-card-content">
      <div class="product-card-content-items">
        <img :src="this.product.image" :alt="this.product.image" width="200px" height="300px" />
      </div>
      <div class="product-card-content-items">
        <div class="text-content">
          <div class="product-title">{{ this.product.title }}</div>
          <div class="product-details">
            <div class="category-rating">
              <div class="category">{{ this.product.category }}</div>
              <div class="rating-circles">
                <p>{{ this.product.rating.rate }}</p>
                <div
                  v-for="i in 5"
                  :key="i"
                  class="circle"
                  :style="{ backgroundColor: getFilledColor(i) }"
                ></div>
              </div>
            </div>
            <hr />
            <div class="product-description">{{ this.product.description }}</div>
            <hr />
            <button @click="getNextProduct" :disabled="loading">Next Product</button>
            <p class="product-price">${{ this.product.price }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
.rating-circles {
  display: flex;
  margin: 10px;
}
.circle {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  margin: 1px;
  border: 2px solid #000; /* Warna default lingkaran */
  align-self: flex-end;
  transform: translate(0%, -70%);
}
</style>
