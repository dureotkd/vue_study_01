<template>
  <!-- <div class="black-bg" v-if="showModal">
    <div class="white-bg">
      <h2>모달입니다</h2>
      <p>매물 : {{ productDetail.name }}</p>
      <p>가격 : {{ productDetail.cost }}</p>
      <p>위치 : {{ productDetail.location }}</p>
      <p>신고수 : {{ productDetail.repoertCnt }}</p>
    </div>
  </div> -->

  <Modal :productDetail="productDetail" :showModal="showModal" />
  <header class="menu">
    <div class="" style="display: flex; justify-content: center">
      <h4 v-for="value in menu" :key="value">{{ value }}</h4>
    </div>
    <div class="">
      <h1 class="red" :style="style">원룸샵</h1>
      <Hello />
    </div>
  </header>
  <main>
    <div v-for="(value, key) in products" :key="value.index">
      <p>번호 : {{ key }}</p>
      <img
        :src="value.img"
        alt="매물 이미지"
        v-on:click="hadleModal($event)"
        :data-index="value.index"
      />
      <p>매물 : {{ value.name }}</p>
      <p>가격 : {{ value.cost }}</p>
      <p>위치 : {{ value.location }}</p>
      <p>신고수 : {{ value.repoertCnt }}</p>
      <button v-on:click="value.repoertCnt += 1" :data-index="value.index">
        허위매물신고
      </button>
    </div>
  </main>
</template>

<script>
import Modal from "./components/Modal.vue";
import Hello from "./components/Hello.vue";

export default {
  name: "App",
  data() {
    return {
      price1: 60,
      price2: 90,
      showModal: false,
      menu: ["Home", "Shop", "About"],
      products: [
        {
          index: 0,
          name: "역삼동",
          cost: 3000,
          location: "역삼동 3번지",
          repoertCnt: 0,
          img: "https://oneroommaking.com/file_data/oneroommake/2018/12/06/7a0f3a857f96c310e29b7c9895902035.jpg",
        },
        {
          index: 1,
          name: "용두동",
          cost: 1000,
          location: "용두동 3번지",
          repoertCnt: 0,
          img: "http://mstatic1.e-himart.co.kr/contents/content/upload/display/306/cont24.jpg",
        },
        {
          index: 2,
          name: "한남동",
          cost: 5000,
          location: "한남동 3번지",
          repoertCnt: 0,
          img: "http://www.ujeil.com/news/photo/201904/230466_83656_442.jpg",
        },
      ],
      productDetail: {},
      style: "color:blue !Important",
    };
  },
  methods: {
    hadleModal: function (event) {
      // 이제 네이티브 이벤트에 액세스 할 수 있습니다

      const dataIndex = event.target.getAttribute("data-index");

      this.productDetail = this.products[dataIndex];
      this.showModal = true;
    },
    // handleModal: function (msg, event) {
    //   this.showModal = true;
    // },
  },
  // useEffect와 비슷
  created() {
    document.addEventListener("click", (event) => {
      if (event.target.className === "black-bg") {
        this.showModal = false;
      }
    });
  },
  components: {
    // '컴포넌트 이름': 컴포넌트 내용
    Modal,
    Hello,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.menu {
  display: flex;
  justify-content: center;
  margin: 0px auto;
  flex-direction: column;
}
.menu h4 {
  margin-left: 8px;
}

main > div {
  margin-bottom: 30px;
}

main > div > img {
  width: 200px;
  border-radius: 15px;
}

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
</style>
