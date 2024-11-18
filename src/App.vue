<!-- 메인브랜치에서 수정 -->
<template>
  <header>
    <div class="menu">
      <a v-for="headerMenu in menus" :key="headerMenu">{{headerMenu}}</a>
    </div>
  </header>
  <div class="products-list" v-for="(a,i) in products" :key="i">
    <h4>{{products[i].name}}</h4>
    <p>{{products[i].price}}</p>
    <button @click="increase(i)">허위매물신고</button>
    <button @click="isModalOpen = true">모달창 열기</button>
    <span>{{warn[i]}}</span>
  </div>

  <div>
    <DiscountBanner></DiscountBanner>
    <h4>{{oneroomData}}</h4>
  </div>

  <!-- 중첩 IF문 -->
  <div v-if="1 == 2">
    안녕하세요
  </div>
  <div v-else-if="3==3">
    중첩IF문
  </div>
  <!-- .// 중첩 IF문 -->


  <!-- 상품 정보 -->
  <div class="img-box" v-for="(a,i) in oneroomData" :key="i">
    <img :src="oneroomData[i].image" class="room-img">
    <h4 @click="isModalOpen = true; modalNum = i">{{oneroomData[i].title}}</h4>
    <p>{{oneroomData[i].content}}</p>
    <span>{{oneroomData[i].price}}원</span>
  </div>
  <!-- .// 상품 정보 -->


  <div class="black-bg" v-if="isModalOpen == true" >
    <div class="white-bg">
      <h4>{{oneroomData[modalNum].title}}</h4>
      <p>상세페이지 내용</p>
      <button @click="isModalOpen = false">닫기</button>
    </div>
  </div>

</template>

<script>

/* 컴포넌트 가지고 오기 */
import DiscountBanner from './components/DiscountBanner.vue'
/* 데이터 가지고 오기 */
import oneroom from './assets/oneroom'

export default {
  data(){
    return { 
      modalNum : 0, /* 값 저장 */
      isModalOpen : false,
      oneroomData : oneroom,
      menus : ['home', 'shop', 'about'],
      products : [{name:'천호동 원룸' , price: '35,000'} , {name: '잠실역 원룸' ,price : '32,000'},  {name: '객체역 원룸' ,price : '15,000'} ],
      warn : [0,1,2],
    }
  },
  methods : {
    increase(i){
      this.warn[i] += 1
    },
  },

  components : {
    DiscountBanner : DiscountBanner,
  }

}
</script>

<style>
  /* common */
  * {box-sizing: border-box;}
  body {margin: 0; padding: 0;}
  header .menu {display: flex; padding: 20px; background: #eee; color: #000; gap: 80px;}
  header .menu > a {font-weight: 700;}
  header .menu > a:hover {background: gray;}

  .tit {cursor: pointer;}
  #app {max-width: 1280px; margin: 0px auto;}

  .img-box {width: 600px; margin: 0px auto;}
  .img-box h4 {cursor: pointer;}
  .room-img {max-width: 100%; margin-top: 40px; width: 100%;}
  /* modal */
  .black-bg {
  width: 100%; height:100%;
  background: rgba(0,0,0,0.5);
  position: fixed; padding: 20px;
  left: 0;
  top: 0;
  }
  .white-bg {
    width: 100%; background: white;
    border-radius: 8px;
    padding: 20px;
  } 
    .discount-banner {background: #eee;}
</style>
