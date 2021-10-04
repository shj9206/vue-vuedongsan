<template>
  <div>
    <img :src="products[index].image" class="room-img" />
    <h4 @click="$emit('openModal', products[index].id)">
      {{ products[index].title }}
    </h4>
    <p>{{ products[index].price }} 만원</p>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: {
    products: Array,
    index: Number,
  },
};
</script>

<style></style>
