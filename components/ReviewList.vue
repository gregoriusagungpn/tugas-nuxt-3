<template>
  <div class="review-container">
    <div class="review-list">
      <h3>Reviews:</h3>
      <ul>
        <li v-for="(review, index) in reviews" :key="index">
          {{ review.name }} gave this {{ review.rating }} stars
          <br />
          "{{ review.review }}"
        </li>
      </ul>
    </div>
  </div>
</template>

<script lang="ts">
export default defineComponent({
  props: {
    reviews: {
      type: Object,
      required: true,
    },
  },
});
</script>

<style>
.review-container {
  display: block;
  margin: 10px;
}

.review-list {
  padding: 5px;
}
</style>
