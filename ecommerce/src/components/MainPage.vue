<script>
import SkeletonLoading from './SkeletonLoading.vue'
import ProductDisplay from './ProductDisplay.vue'

export default {
  components: {
    SkeletonLoading,
    ProductDisplay
  },
  data() {
    return {
      product: {
        title: '',
        rating: { rate: 0, count: 0 },
        image: '',
        category: '',
        price: '',
        description: ''
      },
      loading: false,
      number: 0,
      category: '',
      fontInCardColor: '#002772'
    }
  },

  methods: {
    async getNextProduct() {
      this.loading = true
      try {
        if (this.number === 20) this.number = 0

        this.number = this.number + 1
        // Panggil API untuk mendapatkan produk berikutnya
        this.loading = true
        const response = await fetch(`https://fakestoreapi.com/products/${this.number}`)

        const data = await response.json()

        this.product = data
        switch (data.category) {
          case "men's clothing":
            this.category = 'men'

            break
          case "women's clothing":
            this.category = 'women'
            break
          default:
            this.category = 'nonGender'
        }
      } catch (error) {
        console.error('Error fetching product:', error)
      } finally {
        this.loading = false
      }
    },

    HandlerGetNextProduct() {
      this.getNextProduct()
    }
  },
  watch: {
    category(value) {
      if (value == 'men') {
        document.body.style.backgroundColor = '#D6E6FF'
        document.body.style.backgroundImage = "url('../../public/bg-pattern.png')"
        // document.body.style.background = 'linear-gradient(to bottom, #D6E6FF 70%, #FFFF 100%)'

        this.fontInCardColor = '#002772'
      } else if (value == 'women') {
        document.body.style.backgroundColor = '#FDE2FF'
        document.body.style.backgroundImage = "url('../../public/bg-pattern.png')"
        this.fontInCardColor = '#720060'
      } else {
        document.body.style.backgroundColor = '#dcdcdc'
        document.body.style.backgroundImage = 'none'
      }
    }
  },
  mounted() {
    // Panggil metode untuk mendapatkan produk pertama saat komponen dimuat
    this.getNextProduct()
  }
}
</script>

<template>
  <!-- Product Card Component -->
  <div v-if="this.loading">
    <SkeletonLoading />
  </div>
  <div v-else>
    <ProductDisplay
      :product="this.product"
      :category="this.category"
      :fontInCardColor="this.fontInCardColor"
      :clickGetNextProduct="this.HandlerGetNextProduct"
    />
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
