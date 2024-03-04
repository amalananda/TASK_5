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
    clickGetNextProduct: Function,
    fontInCardColor: String
  },
  data() {
    return {
      bodyBackGroundColor: 'black'
      // elements: [{ content: this.title, backgroundColor: 'pink' }]
    }
  },
  methods: {
    getFilledColor(index) {
      // let color

      // choose color base on category
      // switch (this.category) {
      //   case 'men':
      //     color = '#002772'
      //     break
      //   case 'women':
      //     color = '#720060'
      //     break
      //   case 'nonGender':
      //     color = '#dcdcdc'
      //     break
      // }

      const ceil_number = Math.ceil(this.product.rating.rate)

      // colored bullet by on rating number
      if (index <= ceil_number) {
        return this.fontInCardColor
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
}
</script>

<template>
  <!-- Product Card Component -->

  <div v-if="this.category == 'nonGender'">
    <div class="uncategorized">
      <img src="../assets/sad-face.png" width="660px" height="380px" />
      <p>This product is unavailable to show</p>
      <button @click="getNextProduct">Next Product</button>
    </div>
  </div>

  <div v-else class="product-card">
    <div class="product-card-content">
      <div class="product-card-content-items">
        <img :src="this.product.image" :alt="this.product.image" width="200px" height="300px" />
      </div>
      <div class="product-card-content-items">
        <div class="text-content">
          <div class="product-title" :style="{ color: this.fontInCardColor }">
            {{ this.product.title }}
          </div>
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
            <p class="product-price" :style="{ color: this.fontInCardColor }">
              ${{ this.product.price }}
            </p>

            <button
              class="buy-now"
              @click="getBuyNow"
              :style="{
                backgroundColor: this.fontInCardColor,
                borderColor: this.fontInCardColor
              }"
            >
              Buy Now
            </button>

            <button
              class="next-product"
              @click="getNextProduct"
              :style="{
                color: this.fontInCardColor,
                borderColor: this.fontInCardColor
              }"
            >
              Next Product
            </button>
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

.uncategorized {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 700px; /* Sesuaikan lebar kartu dengan kebutuhan */
  height: 400px; /* Sesuaikan tinggi kartu dengan kebutuhan */
  background-color: white;
  border-radius: 10px;
  border: 3px;
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.2);
}

.uncategorized img {
  display: flex;
  align-items: top;
  padding: 20px;
  height: 300px;
  transform: translate(6%, 10%);
  position: relative;
}

.uncategorized p {
  margin: 10px;
  top: 0;
  right: 0;
  font-family: 'Inter';
  font-size: 13px;
  height: 30px;
  transform: translate(33%, -670%);
}

.uncategorized button {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-52%, -100%);
  background-color: white;
  width: 300px;
  height: 25px;
  border-radius: 5px;
}
</style>
