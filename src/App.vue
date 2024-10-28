<template>
  <header>
      <nav>
        <ul>
          <li v-for="(a,i) in navbar" :key='i'>
            <a href="#">{{navbar[i]}}</a>
          </li>
        </ul>
      </nav>
  </header>
    <div class="black-bg" v-if="isModalOpen == true">
  <div class="white-bg">
    <h4>상세페이지</h4>
    <p>상세페이지내용임</p>
    <button @click='isModalOpen = false'>모달창 닫기</button>
  </div>
  </div>
  <div v-for="(a,i) in products" :key="i">
    <img src="./assets/room0.jpg" alt="" class="room-img">
    <h4 class="tit" @click='isModalOpen = true'>{{products[i]}}</h4>
    <p>XX 만원</p>
    <button @click='increase(i)'>허위매물신고</button>
    <span> 신고수 : {{신고수[i]}}</span>
  </div>

  <div>
    {{oneroom}}
  </div>

</template>

<script>

import data from './assets/oneroom.js'

export default {
  name: 'App',
  data() {
    return  {
      oneroom : data,
      신고수 : [0,0,0],
      메뉴들 : ['', '', ''],
      products : ['역삼동 원룸' , '잠실역 원룸' , '마포구 원룸'],
      navbar : ['home' , 'about', 'skills', 'mypage'],
      isModalOpen : false, 
    }
  },
  methods : {
    increase(i){
      this.신고수[i] += 1
    }
  }
}
</script>

<style>
  * {box-sizing: border-box;}
  body {margin: 0;}
  .tit {cursor: pointer;}
  #app {max-width: 1280px; margin: 0px auto;}
  header > nav > ul {display: flex; gap: 80px; list-style: none; background: aliceblue; padding: 20px;}
  .room-img {max-width: 100%; margin-top: 40px;}
  .black-bg {
  width: 100%; height:100%;
  background: rgba(0,0,0,0.5);
  position: fixed; padding: 20px;
  }
  .white-bg {
    width: 100%; background: white;
    border-radius: 8px;
    padding: 20px;
  } 

</style>
