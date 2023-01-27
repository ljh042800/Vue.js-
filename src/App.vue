<template>
<!-- 동적인 UI 만드는법 
0. 디자인 해두고.
1. UI의 현재 상태를 데이터로 저장해둠.
2. 데이터에 따라 UI가 어떻게 보일지 작성.-->

<!-- v-if = "조건식" 
조건식이 참일때만 HTML 보여준다.-->

<!-- <div v-if="1==2"> 참일때이거
    안녕하세요   
</div>
<div v-else> 참이아닐때 이거
    안녕하세요2
</div> -->

<div class="black-bg" v-if="모달창열렸니 == true">       <!--모달창열렸니가 true일때만 보임. -->
  <div class="white-bg">
    <img :src="원룸들[누른거].image" style="width:100%">
    <h4>{{원룸들[누른거].title}}</h4>
    <p>{{원룸들[누른거].content}}</p>
    <p>{{원룸들[누른거].price}}원</p>
    <Modal/>
    <Discount/>
    <button type="button" @click="모달창열렸니 = false">닫기</button>
  </div>

</div>

<!-- HTML -->
  
  <div class="menu">
    <!-- 반복문: 태그 v-for="??in??"  작명 in 몇회<-이자리에 데이터(자료안의 데이터 갯수만큼 반복) 집어넣어도됨.
    작명한 변수는 데이터안의 자료가 됨.     :key="작명"도 필수 반복문을 구분하기위해서. 
    왼쪽변수는 array내의 데이터 오른쪽 변수는 1씩증가하는 정수.-->
    <!-- <a v-for="(a,i) in 메뉴들" :key="i">{{i}}</a> -->
    <a v-for="i in 메뉴들" :key="i">{{i}}</a>
    
  </div>


  <!-- 축약해둔 컴포넌트 쓰는 법
  vue파일 import 해오고, 등록하고, 쓰면됨. -->
 
 <!-- <Discount/> -->




  <!-- <div v-for="(a,p) in products" :key="p"> -->
    <!--  HTML 속성도 데이터 바인딩 가능.  ex) :속성 = "데이터이름" -->
    <!-- <h4>{{products[p]}}</h4>
    <p>{{ price1[0] }}만원</p>
  </div> -->
  <div v-for="(one,oneroom) in 원룸들" :key="oneroom">
    <!-- HTML 태그안의 속성 데이터 바인딩은 :어쩌구
        HTML 태그안의 내용 데이터 바인딩은 {{어쩌구}} -->
    <img :src="원룸들[oneroom].image" class="room-img">
    <h4 @click="모달창열렸니 = true; 누른거 = oneroom">{{원룸들[oneroom].title}}</h4>
    <p>{{원룸들[oneroom].price}}원</p>
      <!-- 버튼누를때마다 1씩 증가 -->
    <button @click="신고수[0]++">허위매물신고</button> <span>신고수 : {{신고수[0]}}</span>
  </div>
    <!-- <div>
      <img src="./assets/room1.jpg" class="room-img">
    <h4>{{원룸들[1].title}}</h4>
    <p>{{원룸들[1].price}}</p>
    <button @click="신고수[1]++">허위매물신고</button> <span>신고수 : {{신고수[1]}}</span>
  </div>
    <div>
      <img src="./assets/room2.jpg" class="room-img">
    <h4>{{products[2]}}</h4>
    <p>50만원</p>
     <button @click="신고수[2]++">허위매물신고</button> <span>신고수 : {{신고수[2]}}</span>
  </div> -->


</template>


<script>

// document.getElementById().innerHTML = ??; 원래 데이터 집어넣기.
//  function 어쩌구() {
//   console.log('adwadwadawd');
//    console.log('adwadwadawd');
   
//    어쩌구()만 쓰면 안에있는 데이터가 다 나옴.
// }

//  data(): 데이터  저장 통. Object형식으로 왼쪽에 이름 오른쪽에 값. {자료이름 : 자료내용}

// import / export 문법 쓰는법
// 1. export default 변수명 , 2.import 변수명 from 그파일 경로
// import apple from './assets/oneroom.js';
//  import {변수1,변수2} from 경로  //중괄호로했으면 중괄호로가져와야함.
// apple;

import data from './assets/oneroom.js';
import Discount from './Discount.vue';
import Modal from './Modal.vue';


export default {
  name: 'App',
  data(){
    return{
      // import한 data를 가져옴.
      누른거 : 0,
      원룸들 : data,
      모달창열렸니 : false,
      신고수 : [0,0,0],
      price1 : ['60','70','80'],
      스타일 : 'color : blue',
      products: ['역삼동원룸', '천호동원룸' , '마포구원룸'],
      메뉴들 : ['Home','Shop','About'],


      
      
    }
  },
  // methods : {
  //   increase(){
  //     // 함수 안에서 데이터를 쓸땐 this.데이터명
  //     this.신고수[0] += 1;
  //   },
  //   increase1(){
  //     this.신고수[1] +=1;
  //   },
  //   increase2(){
  //     this.신고수[2] +=1;
  //   }
    

  // },

  components: {
    // Discount라는 이름으로 위에서 import한 Discount라는 이름을 가져다 쓰겠다.
    // 왼쪽에 언제나 자유작명 ,왼쪽 오른쪽 이름이 같으면 축약해됨.
    Discount : Discount,
    Modal : Modal,
  }
}
</script>
<style>
body{
  margin : 0
}
div{
  box-sizing: border-box;
}
.discount{
  background: #eee;
  padding: 20px;
  margin: 10px;
  border-radius: 5px;
}
.black-bg {
  width: 100%; height: 100%;
  background: rgba(0,0,0,0,5);
  position: fixed; padding: 20px;
}
.white-bg{
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}




.room-img {
  width: 100%;
  margin-top: 40px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu{
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  padding: 10px;
}
</style>
