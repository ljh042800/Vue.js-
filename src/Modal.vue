<template>
<div class="black-bg" v-if="모달창열렸니 == true">       <!--모달창열렸니가 true일때만 보임. -->
  <div class="white-bg">
    <img :src="원룸들[누른거].image" style="width:100%">
    <h4>{{원룸들[누른거].title}}</h4>
    <p>{{원룸들[누른거].content}}</p>
    <p>{{원룸들[누른거].price}}원</p>
    <button type="button" @click="모달창열렸니 = false">닫기</button>
  </div>

</div>
  

</template>

<script>
export default {
    name : 'Modal',


}
</script>

<style>

</style>