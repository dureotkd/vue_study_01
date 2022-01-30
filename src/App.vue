<template>
  <div>
    <transition name="fade">
      <Modal
        :productDetail="productDetail"
        :showModal="showModal"
        @addReport="addReport"
        :allChk="allChk"
        @handleMemo="handleMemo"
      />
    </transition>
    <header class="menu">
      <div class="" style="display: flex; justify-content: center">
        <h4 v-for="value in menu" :key="value">{{ value }}</h4>
      </div>
      <div class="" style="margin-bottom: 20px">
        <h1 class="red" :style="style">원룸샵</h1>
        <label>
          <input type="checkbox" id="allChk" v-on:change="testAllChk($event)" />
          전체 체크
        </label>
        <button v-on:click="deleteList($event)">삭제</button>
      </div>
    </header>
    <main>
      <List
        :products="products"
        :handleModal="handleModal"
        @test="test"
        @unitChk="unitChk"
        :allChk="allChk"
      />
    </main>
  </div>
</template>

<script>
import Modal from './components/Modal.vue';
import List from './components/List.vue';

export default {
  name: 'App',
  data() {
    return {
      menu: ['Home', 'Shop', 'About'],
      showModal: false,
      allChk: false,
      chkIndex: [],
      products: [
        {
          index: 0,
          name: '역삼동',
          cost: 3000,
          location: '역삼동 3번지',
          repoertCnt: 0,
          img: 'https://oneroommaking.com/file_data/oneroommake/2018/12/06/7a0f3a857f96c310e29b7c9895902035.jpg',
          memo: null,
          checked: false,
        },
        {
          index: 1,
          name: '용두동',
          cost: 1000,
          location: '용두동 3번지',
          repoertCnt: 0,
          img: 'http://mstatic1.e-himart.co.kr/contents/content/upload/display/306/cont24.jpg',
          memo: null,
          checked: false,
        },
        {
          index: 2,
          name: '한남동',
          cost: 5000,
          location: '한남동 3번지',
          repoertCnt: 0,
          img: 'http://www.ujeil.com/news/photo/201904/230466_83656_442.jpg',
          memo: null,
          checked: false,
        },
      ],
      productDetail: {},
      style: 'color:blue !Important',
    };
  },
  methods: {
    deleteList: function () {
      this.products = this.products.filter((value) => {
        return value.checked ? false : true;
      });
    },
    addReport: function () {
      this.productDetail.repoertCnt += 1;
    },
    handleModal: function (event) {
      const dataIndex = event.target.getAttribute('data-index');

      this.productDetail = this.products[dataIndex];
      this.showModal = true;
    },
    handleMemo: function (event) {
      const onlyNumber = event.target.value.replace(/[^0-9]/g, '');
      this.productDetail.memo = onlyNumber;

      return onlyNumber;
    },
    test: (event) => {
      alert(event.target.className);
    },
    testAllChk: function (event) {
      const isChk = event.target.checked;

      this.products.map((value) => {
        value.checked = isChk ? true : false;
      });
    },
    unitChk: function (event) {
      const isChk = event.target.checked;
      const dataIndex = event.target.getAttribute('data-index');

      this.products[dataIndex].checked = isChk;

      return event;
    },
  },
  // useEffect와 비슷
  created() {
    document.addEventListener('click', (event) => {
      if (event.target.className === 'black-bg') {
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
.fade-enter-from {
  opacity: 0;
}
.fade-enter-active {
  transition: all.6s;
}
.fade-enter-to {
  opacity: 1;
}
.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: all.6s;
}
.fade-leave-to {
  opacity: 0;
}
</style>
