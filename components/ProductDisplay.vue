<template>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <img
          :src="productImage"
          :class="[!inStock ? 'out-of-stock-img' : '']"
        />
      </div>
      <div class="product-info">
        <h1>{{ title }}</h1>
        <p>
          {{ productDescription }}
          <br />
          <a :href="productUrl" target="_blank">visit our website</a>
        </p>
        <p v-if="inStock">In Stock</p>
        <p v-else>Out of Stock</p>
        <p>Shipping: {{ premium ? "Free" : "2.99" }}</p>
        <ul>
          <li v-for="detail in details">{{ detail }}</li>
        </ul>
        <div
          v-for="(variant, index) in variants"
          :key="variant.id"
          @mouseover="updateVariant(index)"
          class="color-circle"
          :style="{ backgroundColor: variant.color }"
        ></div>
        <br />
        <button class="button" @click="addToCart" :disabled="!inStock">
          Add to cart
        </button>
      </div>
    </div>
  </div>
  <ReviewList v-if="reviews.length" :reviews="reviews"></ReviewList>
  <ReviewForm @review-submitted="addReview"></ReviewForm>
</template>

<script setup lang="ts">
const product = "Socks";

const brand = "Adimas";

const productDescription = "Comfortable socks for your daily use";

const productUrl = "https://marelsp.com";

const onSale = true;

const details = ["50% cotton", "30% wool", "20% polyester"];

const selectedVariant = ref(0);

const variants = [
  {
    id: 2234,
    color: "green",
    image: "assets/images/socks_green.jpg",
    quantity: 20,
  },
  {
    id: 2235,
    color: "blue",
    image: "assets/images/socks_blue.jpg",
    quantity: 0,
  },
];

const arrReview: Array<Object>[] = [];

const reviews = ref(arrReview);

const updateVariant = (index: number) => {
  selectedVariant.value = index;
  // console.log(index);
};

const title = computed(
  () => brand + " " + product + [onSale ? " is on sale" : ""]
);

const productImage = computed(() => variants[selectedVariant.value].image);

const inStock = computed(() => variants[selectedVariant.value].quantity);

const emit = defineEmits(["add-to-cart"]);

const addToCart = () => {
  emit("add-to-cart", variants[selectedVariant.value].id);
};

const addReview = (review: Array<Object>) => {
  reviews.value.push(review);
};
</script>

<script lang="ts">
export default defineComponent({
  props: {
    premium: {
      type: Boolean,
      required: true,
    },
  },
});
</script>

<style>
.product-display {
  display: inline-block;
  margin: 10px;
}

.product-image {
  float: left;
  border: 2px solid;
  margin: 10px;
}

.product-info {
  float: left;
  margin: 5px;
}

.color-circle {
  width: 50px;
  height: 50px;
  margin-top: 8px;
  border: 2px solid #d8d8d8;
  border-radius: 50%;
}

.disabled-button {
  background-color: #d8d8d8;
  cursor: not-allowed;
}

.out-of-stock-img {
  filter: opacity(0.5) drop-shadow(0 0 gray);
}
</style>
