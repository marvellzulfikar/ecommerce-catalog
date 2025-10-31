<script>
export default {
  name: "ProductButton",
  props: {
    category: {
      type: String,
      required: true,
    },
    nextProduct: {
      type: Function,
      required: true,
    },
  },
  computed: {
    leftButtonColor() {
      return this.category === "women's clothing" ? "#720060" : "#002772";
    },
    leftButtonTextColor() {
      return "white";
    },

    rightButtonBorderColor() {
      return this.category === "women's clothing" ? "#720060" : "#002772";
    },
    rightButtonTextColor() {
      return this.category === "women's clothing" ? "#720060" : "#002772";
    },
  },
  methods: {
    handleNextProduct() {
      this.nextProduct();
    },
  },
};
</script>

<template>
  <div class="button-container">
    <button
      :style="{ backgroundColor: leftButtonColor, color: leftButtonTextColor }"
      class="dynamic-button buy-button">
      Buy Now
    </button>

    <button
      @click="handleNextProduct"
      :style="{
        backgroundColor: rightButtonColor,
        border: `2px solid ${rightButtonBorderColor}`,
        color: rightButtonTextColor,
      }"
      class="dynamic-button next-button"
    >
      Next Product
    </button>
  </div>
</template>

<style scoped>
.button-container {
  display: flex;
  justify-content: space-between;
  margin: 20px;
}

.dynamic-button {
  padding: 10px 20px;
  cursor: pointer;
  font-size: 20px;
  transition: background-color 0.3s ease, color 0.3s ease;
  border: none;
  width: 260px;
  height: 45px;
  top: 620px;
  left: 600px;
}

.buy-button:hover {
  filter: brightness(90%);
}

.next-button {
  background-color: white;
}

.next-button:hover {
  background-color: #e5e5e5;
}
</style>
