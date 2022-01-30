<template>
  <div class="black-bg" v-if="showModal && productDetail">
    <div class="white-bg">
      <h2>상세정보</h2>
      <img class="room-img" :src="productDetail.img" alt="매물 이미지" />
      <p>매물 : {{ productDetail.name }}</p>
      <p>가격 : {{ productDetail.cost }}</p>
      <p>위치 : {{ productDetail.location }}</p>
      <p>신고수 : {{ productDetail.repoertCnt }}</p>
      <div
        class=""
        style="margin-bottom: 20px; display: flex; justify-content: center"
      >
        <p>메모</p>
        <input
          type="text"
          autofocus
          v-on:change="$emit('handleMemo', $event)"
          :value="productDetail.memo"
        />
      </div>
      <button
        :data-index="productDetail.index"
        v-on:click="$emit('addReport', $event)"
      >
        허위매물신고
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Modal',
  data() {},
  watch: {},
  methods: {},
  props: {
    showModal: Boolean,
    productDetail: Object,
  },
};
</script>

<style>
.room-img {
  width: 400px;
  border-radius: 12px;
}
</style>
