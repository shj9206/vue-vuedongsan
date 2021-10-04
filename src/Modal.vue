<template>
  <div class="black-bg" v-if="openModal == true">
    <div class="white-bg">
      <h4>{{ products[modalIndex].title }}</h4>
      <p>{{ products[modalIndex].content }}</p>
      <!-- <input @input="month = $event.target.value" /> -->
      <input v-model="month" />
      <p>{{ month }}개월 선택 : {{ products[modalIndex].price * month }}원</p>

      <button @click="closeModal">
        닫기
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  data() {
    return {
      month: 1,
    };
  },
  watch: {
    month(a) {
      if (a > 13) {
        alert("13이상 입력하지 마세요");
        return;
      }
      if (isNaN(a) == true) {
        alert("글자는 입력하지 마세요");
        this.month = 1;
      }
    },
  },

  props: {
    products: Array,
    modalIndex: Number,
    openModal: Boolean,
  },
  methods: {
    closeModal() {
      this.$emit("closeModal", this.products[this.modalIndex].id);
      this.month = 1;
    },
  },
};
</script>

<style></style>
