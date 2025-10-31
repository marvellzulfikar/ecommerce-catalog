<script>
export default {
  name: "RatingProduct",
  props: {
    rating: {
      type: Number,
      required: true,
    },
    ratingColor: {
      type: String,
      default: "#002772",
    },
  },
};
</script>

<template>
  <div class="rating-container">
    <span class="rating-value">{{ rating }}/5</span>
    <div class="stars-container">
      <div
        v-for="star in 5"
        :key="star"
        class="star"
        :style="{
          backgroundColor: star <= Math.round(rating) ? ratingColor : '#e0e0e0',
        }"
      ></div>
    </div>
  </div>
</template>

<style scoped>
.rating-container {
  display: flex;
  align-items: center;
}

.rating-value {
  margin-right: 10px;
  font-size: 1em;
}

.stars-container {
  display: flex;
  gap: 3px;
}

.star {
  width: 20px;
  height: 20px;
  clip-path: polygon(
    50% 0%,
    61% 35%,
    98% 35%,
    68% 57%,
    79% 91%,
    50% 70%,
    21% 91%,
    32% 57%,
    2% 35%,
    39% 35%
  );
}
</style>
