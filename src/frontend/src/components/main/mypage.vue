<template>

<div class="wrap">
  <div class="greenContainer">
    <div>
      <div class="name">{{ this.$store.state.userStore.id }} 님</div>
      {{this.$store.state.careprofileStore.activityTime}} 
    </div>    
  </div>
  <div class="listContainer">
    <div v-if="this.$store.state.userStore.careSitterId == null || this.$store.state.careprofileStore.activityTime == null" >
      <a  class="item">
        <div class="icon">ii</div>
        <router-link :to="{name:'careprofilecreate'}"><div class="text">케어 프로필 생성</div></router-link>
        <div class="right"> > </div>
      </a>
    </div>
    <div v-else>
      <a  class="item" >
        <div class="icon" >ii</div>
        <router-link :to="{name:'certification',params:{caresitterId:this.id}}"><div class="text">자격증 등록<span class="circle"></span></div></router-link>
        <div class="right"> > </div>
    </a>
    <a  class="item"> 
        <div class="icon">ii</div>
        <router-link :to="{name:'mypage_certi' ,params:{caresitterId:this.id}}"><div class="text">케어 자격증 조회</div></router-link>
        <div class="right"> > </div>
    </a>
    <a  class="item">
        <div class="icon">ii</div>
        <router-link :to="{name:'mypage_profile' ,params:{caresitterId:this.id}}"> <div class="text">프로필 조회</div></router-link>
        <div class="right"> > </div>
    </a>
    </div>
    <a  class="item">
        <div class="icon">ii</div>
        <router-link :to="{name:'Caretargets'}"><div class="text">케어 대상인 조회</div></router-link>
        <div class="right"> > </div>
    </a>
    <a  class="item">
        <div class="icon">ii</div>
         <router-link :to="{name:'mypage_joblist'}"><div class="text">내 구인공고 관리</div></router-link>
        <div class="right"> > </div>
    </a>
    <a  class="item">
        <div class="icon">ii</div>
          <router-link :to="{name:'MyStore',params:{contentId:memid}}"><div class="text">내 스토어</div></router-link>
        <div class="right"> > </div>
    </a>
    <a  class="item">
        <div class="icon">ii</div>
         <router-link :to="{name:'OrderList',params:{contentId:memid}}"><div class="text">상품 주문 내역</div></router-link>
        <div class="right"> > </div>
    </a>
    
  </div>
  <div class="listContainer">
    <!-- <a href="#" class="item">
        <div class="icon">ii</div>
        <div class="text">
          <span>내지갑</span>
          <span class="smallLight">
            <span>|</span>
            <span>보유 적립금</span>
          </span>          
        </div>                
        <div class="right">
          <span class="blct">175 BLCT</span>
          > </div>
    </a> -->
    <a  class="item">
        <div class="icon">ii</div>
         <router-link :to="{name:'memberSchedule', params:{caresitterId:this.id}}"><div class="text">스케줄</div></router-link>
        <div class="right"> > </div>
    </a>
    <a  class="item">
        <div class="icon">ii</div>
         <router-link :to="{name:'caresitter_contract', params:{caresitterId:this.id}}"><div class="text">계약서 조회</div></router-link>
        <div class="right"> > </div>
    </a>
    <a  class="item">
        <div class="icon">ii</div>
         <router-link :to="{name:'carenote'}"><div class="text">케어노트(케어시터)</div></router-link>
        <div class="right"> > </div>
    </a>
     <a  class="item">
        <div class="icon">ii</div>
         <router-link :to="{name:'membernote'}"><div class="text">케어노트(회원)</div></router-link>
        <div class="right"> > </div>
    </a>
    <a  class="item">
        <div class="icon">ii</div>
         <router-link :to="{name:'complete_contract'}"><div class="text">완료된 계약서(케어시터)</div></router-link>
        <div class="right"> > </div>
    </a>
    <a  class="item">
        <div class="icon">ii</div>
         <router-link :to="{name:'complete_target'}"><div class="text">완료된 계약서(회원)</div></router-link>
        <div class="right"> > </div>
    </a>
    <a  class="item">
        <div class="icon">ii</div>
         <router-link :to="{name:'adminpage'}"><div class="text">관리자 페이지</div></router-link>
        <div class="right"> > </div>
    </a>


  
  </div>
  <!-- <div class="infoContainer">
    <a href="#" class="item">
      <div>icon</div>
      <div>공지사항</div>
    </a>    
    <a href="#" class="item">
      <div>icos</div>
      <div>공지사항2</div>
    </a>    
    <a href="#" class="item">
      <div>icon</div>
      <div>공지사항3</div>
    </a>
  </div> -->
</div>
 
  

</template>

<script>
export default {
    
    data(){
        return{
            id:this.$store.state.userStore.careSitterId,
            memid:this.$store.state.userStore.id,
            result:[],
        }
    },
    
}
</script>

<style scoped>
a {
  text-decoration: none;
}

body{
  padding: 0;
  margin: 0;
}
div{
  box-sizing: border-box;
}

/* alert badge */
.circle{
  display: inline-block;
  width: 5px;
  height: 5px;
  border-radius: 2.5px;
  background-color: #ff0000;
  position: absolute;
  top: -5px;
  left: 110%;
}

/* 녹색 텍스트 */
.green{
  color: #24855b;
}

.wrap{
  background-color: #F8F8F8;  
}
/* 녹색배경 */
.greenContainer{  
  height: 132px;
  background-color: #616161;    
  
  display: flex;
  align-items: flex-end;
  padding: 16px;
}

.greenContainer .name{
   font-size: 20px;
  font-weight: bold;
  color: #ffffff;
} 
.greenContainer .modify{
  margin-left: auto;
}

/* 단골상점 , 상품후기 , 적립금 박스 */
.summaryContainer{
  background-color: white;  
  display: flex;  
  padding: 21px 16px;  
  height: 90px;
  margin-bottom: 10px;
}
/* 단골상점 , 상품후기 , 적립금 */
.summaryContainer .item{
  flex-grow: 1
}
/* 녹색 숫자 */
.summaryContainer .number{
  font-size: 19px;
  font-weight: bold;
  color: #24855b;
}
/* 텍스트 */
.summaryContainer .item > div:nth-child(2){
  font-size: 13px;
}

/* ================== 주문/배송조회 박스 시작 ==================== */
.shippingStatusContainer{
  padding: 21px 16px;
  background-color: white;
  margin-bottom: 10px;
}

/* 주문/배송조회 타이틀 */
.shippingStatusContainer .title{
  font-size: 16px;
  font-weight: bold;
  margin-bottom: 15px;
}

/* 장바구니 결제완료 배송중 구매확정 [로우] */
.shippingStatusContainer .status{
  display: flex;
  justify-content: space-between;
  margin-bottom: 21px;
}
/* 장바구니 결제완료 배송중 구매확정 [아이템]  */
.shippingStatusContainer .item{
  display: flex;
}

.shippingStatusContainer .number{
  font-size: 31px;
  font-weight: 500;
  text-align: center;
}
.shippingStatusContainer .text{
  font-size: 12px;
  font-weight: normal;
  color: #c2c2c2;
  text-align: center;
}
.shippingStatusContainer .icon{
  display: flex;
  align-items: center;
  padding: 20px;
  width: 16px;
  height: 16px;
}


/*=================== 주문목록 ~ 찜한상품 리스트 ==================*/
.listContainer{  
  padding: 0;
  background-color: #ffffff;
  margin-bottom: 10px;
}
.listContainer .item{  
  display: flex;
  align-items: center;
  padding: 16px;
  color: black;
  text-decoration: none;  
  height: 56px;
  box-sizing: border-box;
}
.listContainer .icon{  
  margin-right: 14px;
}
.listContainer .text{
  font-size: 16px;
  position: relative;
}
.listContainer .right{
  margin-left: auto;
}


/*=================== 내지갑의 보유 적립금 들어가는 부분 ================*/
.listContainer .smallLight{
  font-size: 14px;
  color: #c2c2c2;  
}
.listContainer .smallLight > span{
  margin-left: 10px;
}

.listContainer .right .blct{
  font-size: 14px;
  font-weight: bold;
  margin-right: 5px;
}



/* 공지사항 이용안내 고객센터 */
.infoContainer{
  background-color: white; 
  display: flex;
  height: 100px;
  margin-bottom: 10px;    
}

.infoContainer .item{
  flex-grow: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  font-size: 13px;
  text-decoration: none;
  color: black;
}
.infoContainer .item > div:first-child{
  margin-bottom: 2px;
}



/*  */
.listContainer .item:hover{
/*   background-color: #f8f8f8; */
}
.infoContainer .item:hover{
/*   background-color: #f8f8f8; */
}
</style>