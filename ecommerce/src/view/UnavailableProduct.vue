<script>
export default {
  name: "UnavailableProduct",
  props: {
    handleClick: {
      type: Function,
      required: true,
    },
    buttonName: {
      type: String,
      required: true,
    },
  },
};
</script>

<template>
  <div class="unavailable-product-container">
    <p>This product is unavailable</p>
    <button @click="handleClick">{{ buttonName }}</button>
  </div>
</template>

<style>
.unavailable-product-container {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  background-image: url("@/assets/sad-face.png");
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
  margin-left: 82px;
}

p {
  font-size: 1.5rem;
  color: #333;
  margin-bottom: 50px;
  margin-right: 150px;
}

button {
  width: 465px;
  height: 40px;
  padding: 10px 20px;
  margin-right: 155px;
  font-size: 1rem;
  cursor: pointer;
  background-color: white;
}
</style>
