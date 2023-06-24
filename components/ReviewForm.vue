<template>
  <div class="review-form-container">
    <form class="review-form" @submit.prevent="onSubmit">
      <h3>Leave a review</h3>
      <label for="name">Name:</label>
      <input id="name" v-model="name" />
      <br /><br />

      <label for="review">Review:</label>
      <textarea id="review" v-model="review"></textarea>
      <br /><br />

      <label for="rating">Rating:</label>
      <select id="rating" v-model.number="rating">
        <option>5</option>
        <option>4</option>
        <option>3</option>
        <option>2</option>
        <option>1</option>
      </select>
      <br /><br />

      <input type="submit" class="button" value="Submit" />
      <br /><br /><br /><br /><br /><br />
    </form>
  </div>
</template>

<script setup lang="ts">
const name = ref("");

const review = ref("");

const rating = ref(null);

const emit = defineEmits(["review-submitted"]);

const onSubmit = () => {
  if (name.value === "" || review.value === "" || rating.value === "") {
    alert("Review is incomplete. Please fiil out every field.");
    return;
  }
  let productReview = {
    name: name.value,
    review: review.value,
    rating: rating.value,
  };
  // console.log(productReview);
  emit("review-submitted", productReview);

  name.value = "";
  review.value = "";
  rating.value = null;
};
</script>

<style>
.review-form-container {
  display: block;
  margin: 10px;
}

.review-form {
  padding: 5px;
}
</style>
