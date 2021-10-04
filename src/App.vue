<template>
  <div>
    <div class="start" :class="{ end: openModal }">
      <Modal
        @closeModal="
          openModal = false;
          modalIndex = $event;
        "
        :products="products"
        :modalIndex="modalIndex"
        :openModal="openModal"
      />
    </div>

    <div class="menu">
      <a v-for="(menuName, i) in menu" :key="i">{{ menuName }}</a>
    </div>
    <Discount v-if="openDiscount == true" />
    <button @click="priceSort">가격순 정렬</button>
    <button @click="sortBack">되돌리기</button>
    <div v-for="(item, i) in products" :key="i">
      <Card
        @openModal="
          openModal = true;
          modalIndex = $event;
        "
        :products="products"
        :index="i"
      />
    </div>
  </div>
</template>

<script>
import data from "./assets/data.js";
import Discount from "./Discount.vue";
import Modal from "./Modal.vue";
import Card from "./Card.vue";

export default {
  name: "App",
  data() {
    return {
      openDiscount: true,
      modalIndex: 0,
      openModal: false,
      신고수: 0,
      menu: ["Home", "Shop", "About"],
      initProducts: [...data],
      products: data,
      price1: 60,
      price2: 70,
    };
  },
  methods: {
    increase() {
      this.신고수++;
    },
    priceSort() {
      this.products.sort(function(a, b) {
        return a.price - b.price;
      });
    },
    sortBack() {
      this.products = [...this.initProducts];
    },
  },
  mounted() {
    setTimeout(() => {
      this.openDiscount = false;
    }, 2000);
  },
  components: {
    Discount: Discount,
    Modal,
    Card,
  },
};
</script>

<style>
body {
  margin: 0;
}
div {
  box-sizing: border-box;
}
.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
}
.white-bg {
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}
.room-img {
  width: 100%;
  margin-top: 40px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  padding: 10px;
}
.start {
  opacity: 0;
  transition: all 1s;
}
.end {
  opacity: 1;
}
</style>
