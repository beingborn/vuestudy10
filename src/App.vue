<template>
  <header>
    <div class="menu">
      <a v-for="headerMenu in menus" :key="headerMenu">{{ headerMenu }}</a>
    </div>
  </header>
  <div class="inner">
    <div class="sort-group">
      <button @click="priceSort()">가격순정렬</button>
      <button @click="sortBack()">되돌리기</button>
    </div>
    <!-- 상품 정보 출력 -->
    <div class="img-box" v-for="(a, i) in oneroomData" :key="i">
      <img :src="oneroomData[i].image" class="room-img" />
      <h4
        @click="
          isModalOpen = true;
          modalNum = i;
        "
      >
        {{ oneroomData[i].title }}
      </h4>
      <p>{{ oneroomData[i].content }}</p>
      <span>{{ oneroomData[i].price }}원</span>
    </div>

    <div class="black-bg" v-if="isModalOpen == true">
      <div class="white-bg">
        <h4>{{ oneroomData[modalNum].title }}</h4>
        <p>상세페이지 내용</p>
        <button @click="isModalOpen = false">닫기</button>
      </div>
    </div>
  </div>
  <DiscountBanner></DiscountBanner>
  <ModalItem></ModalItem>
</template>

<script>
import DiscountBanner from "./components/DiscountBanner.vue"; /* 컴포넌트 가지고 오기 */
import ModalItem from "./components/ModalItem.vue";
import oneroom from "./assets/oneroom"; /* 데이터 가지고 오기 */

export default {
  data() {
    return {
      modalNum: 0 /* 값 저장 */,
      isModalOpen: false,
      oneroomDataOrigin: [...oneroom],
      oneroomData: oneroom,
      menus: ["home", "shop", "about"],
      products: [
        { name: "천호동 원룸", price: "35,000" },
        { name: "잠실역 원룸", price: "32,000" },
        { name: "객체역 원룸", price: "15,000" },
      ],
      warn: [0, 1, 2],
    };
  },
  methods: {
    increase(i) {
      this.warn[i] += 1;
    },
    priceSort() {
      this.oneroomData.sort(function (a, b) {
        return a.price - b.price;
      });
    },
    sortBack() {
      this.oneroomData = [...this.oneroomDataOrigin];
    },
  },

  components: {
    DiscountBanner: DiscountBanner,
    ModalItem: ModalItem,
  },
};
</script>

<style>
/* common */
* {
  box-sizing: border-box;
}
body {
  margin: 0;
  padding: 0;
}
header .menu {
  display: flex;
  padding: 20px;
  background: #eee;
  color: #000;
  gap: 80px;
}
header .menu > a {
  font-weight: 700;
}
header .menu > a:hover {
  background: gray;
}
.sort-group {
  margin-top: 12px;
}
.sort-group > button {
  background: purple;
  color: white;
  padding: 12px;
  border-radius: 12px;
  border: none;
}
.sort-group > button + button {
  margin-left: 12px;
}
.tit {
  cursor: pointer;
}
.inner {
  max-width: 1280px;
  margin: 0px auto;
}

.img-box {
  width: 600px;
  margin: 0px auto;
}
.img-box h4 {
  cursor: pointer;
}
.room-img {
  max-width: 100%;
  margin-top: 40px;
  width: 100%;
}
/* modal */
.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
  left: 0;
  top: 0;
}
.white-bg {
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}
</style>
