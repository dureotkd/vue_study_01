<template>
  <div>
    <Modal
      :productDetail="productDetail"
      :showModal="showModal"
      @addReport="addReport"
      @handleMemo="handleMemo"
    />
    <header class="menu">
      <div class="" style="display: flex; justify-content: center">
        <h4 v-for="value in menu" :key="value">{{ value }}</h4>
      </div>
      <div class="">
        <h1 class="red" :style="style">원룸샵</h1>
      </div>
    </header>
    <main>
      <List :products="products" :handleModal="handleModal" @test="test" />
    </main>
  </div>
</template>

<script>
import Modal from "./components/Modal.vue";
import List from "./components/List.vue";

export default {
  name: "App",
  data() {
    return {
      menu: ["Home", "Shop", "About"],
      showModal: false,
      products: [
        {
          index: 0,
          name: "역삼동",
          cost: 3000,
          location: "역삼동 3번지",
          repoertCnt: 0,
          img: "https://oneroommaking.com/file_data/oneroommake/2018/12/06/7a0f3a857f96c310e29b7c9895902035.jpg",
          memo: null,
        },
        {
          index: 1,
          name: "용두동",
          cost: 1000,
          location: "용두동 3번지",
          repoertCnt: 0,
          img: "http://mstatic1.e-himart.co.kr/contents/content/upload/display/306/cont24.jpg",
          memo: null,
        },
        {
          index: 2,
          name: "한남동",
          cost: 5000,
          location: "한남동 3번지",
          repoertCnt: 0,
          img: "http://www.ujeil.com/news/photo/201904/230466_83656_442.jpg",
          memo: null,
        },
      ],
      productDetail: {},
      style: "color:blue !Important",
    };
  },
  methods: {
    handleMemo: function () {},
    addReport: function (event) {
      const dataIndex = event.target.getAttribute("data-index");

      this.productDetail.repoertCnt += 1;
    },
    handleModal: function (event) {
      const dataIndex = event.target.getAttribute("data-index");

      this.productDetail = this.products[dataIndex];
      this.showModal = true;
    },
    handleMemo: function (event) {
      this.productDetail.memo = event.target.value;
    },
    test: (event) => {
      alert(event.target.className);
    },
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
    List,
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
