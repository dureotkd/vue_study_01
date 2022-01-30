<template>
  <div v-for="(value, key) in products" :key="key">
    <div>
      <label>
        <input
          type="checkbox"
          name="asffsa"
          :checked="value.checked ? 'checked' : false"
          v-on:change="$emit('unitChk', $event)"
          :data-index="key"
        />
        삭제
      </label>
    </div>
    <img
      :src="value.img"
      alt="매물 이미지"
      v-on:click="handleModal($event)"
      :data-index="value.index"
    />
    <p>매물 : {{ value.name }}</p>
    <p>가격 : {{ value.cost }}</p>
    <p>위치 : {{ value.location }}</p>
    <p>신고수 : {{ value.repoertCnt }}</p>
    <button class="children" v-on:click="$emit('test', $event)">
      부모한테 이벤트전송
    </button>
    <button v-on:click="value.repoertCnt += 1" :data-index="value.index">
      허위매물신고
    </button>
  </div>
</template>

<script>
export default {
  name: 'List',
  props: {
    products: Array,
    handleModal: Function,
    test: Function,
    allChk: Boolean,
  },
};
</script>
