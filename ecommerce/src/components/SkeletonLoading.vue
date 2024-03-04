<template>
  <!-- Product Card Component -->

  <div class="product-card">
    <div class="product-card-content">
      <div class="product-card-content-items">
        <div class="product-img" width="200px" height="300px"></div>
      </div>
      <div class="product-card-content-items">
        <div class="text-content">
          <div class="product-title"></div>
          <div class="product-details">
            <div class="category-rating">
              <div class="category"></div>
              <div class="rating-circles"></div>
            </div>
            <hr />
            <div class="product-description"></div>
            <hr />
            <p class="product-price"></p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.product-card {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 700px; /* Sesuaikan lebar kartu dengan kebutuhan */
  height: 400px; /* Sesuaikan tinggi kartu dengan kebutuhan */
  background-color: white;
  border-radius: 10px;
}

.product-card-content {
  display: flex;
  align-items: top;
  padding: 20px;
  height: 380px;
}

.product-card .product-img {
  margin-top: 30px;
  width: 200px; /* Set the width of the image */
  height: 300px; /* Maintain the aspect ratio of the image */
  margin-right: 10px; /* Adjust spacing between image and text */
  background-color: #dcdcdc;
}

/* .container {
  position: relative;
  height: 100vh;
} */

.product-title {
  margin: 10px;
  top: 0;
  right: 0;
  width: 400px;
  height: 30px;
  background-color: #dcdcdc;
}

.product-details .category-rating {
  height: 40px;
  /* justify-content: space-between; */
  /* margin-inline: 10px; */
  /* display: flex; */
  /* align-items: center; */
  background-color: #dcdcdc;
  margin-bottom: 10px;
}

.product-details .category {
  /* margin: 10px; */
  top: 0;
  right: 0;
  background-color: #dcdcdc;
  /* overflow: hidden; */
}

.product-details .rating-circles {
  /* justify-content: left; */
  margin: 0px;
}

.product-details hr {
  height: 2px;
  margin-inline: 10px;
  margin-top: 0;
  border-width: 0;
  /* background-color: #dcdcdc; */
}

.product-details p {
  margin: 10px;
  top: 0;
  right: 0;
  background-color: #dcdcdc;
}

.product-description {
  background-color: #dcdcdc;
  margin: 10px;

  height: 150px; /* Set the maximum height for the container */
  /* white-space: nowrap; Prevent text from wrapping to the next line */
}

.product-category {
  background-color: #dcdcdc;
  margin: 10px;
  /* font-weight: bold; */
}
</style>
