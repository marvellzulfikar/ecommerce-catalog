<script>
import LoadingSpinner from "../components/Spin.vue";
import ProductButton from "../components/Button.vue";
import RatingProduct from "../components/Rating.vue";
import UnavailableProduct from "./UnavailableProduct.vue";

export default {
  name: "ProductView",
  components: {
    UnavailableProduct,
    LoadingSpinner,
    RatingProduct,
    ProductButton,
  },
  data() {
    return {
      product: {},
      currentProductId: 15,
      isLoading: false,
    };
  },
  created() {
    this.fetchProduct(this.currentProductId);
  },
  methods: {
    async fetchProduct(productId) {
      this.isLoading = true;
      try {
        const response = await fetch(
          `https://fakestoreapi.com/products/${productId}`
        );
        const data = await response.json();
        this.product = data;
        this.$emit("categoryChanged", data.category);
      } catch (error) {
        console.error("Error fetching product:", error);
      } finally {
        this.isLoading = false;
      }
    },
    fetchNextProduct() {
      this.currentProductId =
        this.currentProductId < 20 ? this.currentProductId + 1 : 1;
      this.fetchProduct(this.currentProductId);
    },
    getDynamicColor(category) {
      return category === "men's clothing"
        ? "#002772"
        : category === "women's clothing"
        ? "#720060"
        : "#002772";
    },
    isValidCategory(category) {
      return category === "men's clothing" || category === "women's clothing";
    },
  },
};
</script>

<template>
  <div class="container">
    <LoadingSpinner :isLoading="isLoading" />
    <div
      v-if="!isLoading && isValidCategory(product.category)"
      class="product-view"
    >
      <div class="image-container">
        <img :src="product.image" alt="Product Image" />
      </div>
      <div class="content-container">
        <div>
          <h1 :style="{ color: getDynamicColor(product.category) }">
            {{ product.title }}
          </h1>
          <div class="category">
            <p class="category-text">{{ product.category }}</p>
            <RatingProduct
              :rating="product.rating.rate"
              :ratingColor="getDynamicColor(product.category)"
            />
          </div>
          <hr />
        </div>
        <div class="description">
          <p>{{ product.description }}</p>
        </div>
        <div>
          <hr />
          <h2 :style="{ color: getDynamicColor(product.category) }">
            ${{ product.price }}
          </h2>
          <div>
            <ProductButton
              :category="product.category"
              :nextProduct="fetchNextProduct"
            />
          </div>
        </div>
      </div>
    </div>
    <UnavailableProduct
      v-else-if="!isLoading && !isValidCategory(product.category)"
      :handleClick="fetchNextProduct"
      buttonName="Next Product"
    />
  </div>
</template>

<style scoped>
.container {
  height: 100%;
}
.product-view {
  display: flex;
  justify-content: space-between;
  gap: 20px;
  padding: 20px;
  height: 100%;
  box-sizing: border-box;
}
.category {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 25px;
}
.description {
  flex: 2;
  overflow: hidden;
  padding: 10px 0;
}
.description p {
  margin: 0;
}

hr {
  margin: 0;
}

.image-container {
  width: 40%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
.image-container img {
  max-width: 70%;
  max-height: 70%;
  height: auto;
  object-fit: cover;
}
.content-container {
  display: flex;
  flex-direction: column;
  width: 60%;
  height: 100%;
  box-sizing: border-box;
}
.content-container > div {
  margin-bottom: 10px;
}
</style>
