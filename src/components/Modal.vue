<template>
  <div class="black-bg" v-if="showModal">
    <div class="white-bg">
      <h2>모달입!!니다</h2>
      <p>매물 : {{ productDetail.name }}</p>
      <p>가격 : {{ productDetail.cost }}</p>
      <p>위치 : {{ productDetail.location }}</p>
      <p>신고수 : {{ productDetail.repoertCnt }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  props: {
    showModal: Boolean,
    productDetail: Object,
  },
};
</script>
