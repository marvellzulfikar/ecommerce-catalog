<script>
export default {
  name: "ProductCard",
};
</script>

<template>
  <div class="card">
    <slot></slot>
  </div>
</template>

<style>
.card {
  width: 1200px;
  height: 600px;
  gap: 0px;
  position: relative;
  justify-content: center;
  align-items: center;
  border-radius: 10px;
  background-color: white;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}
</style>
