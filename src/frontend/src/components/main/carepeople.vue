<template>
<body>
    <div class="container">
        <div class="py-5 text-center">

            <h2>케어 대상인 등록</h2>
            <!-- <p class="lead">케어 대상인 등록</p> -->
        </div>

        <div class="col-md-12 order-md-1">
            <h4 class="mb-3">케어대상인 정보</h4>



                <div class="mb-3">
                    <label for="username">이름</label>
                    <div class="input-group">
                        
                        <input type="text" class="form-control" id="username" placeholder="이름을 입력하세요" v-model="name" required name="user-id">
                    </div>        
                </div>
                
                <div class="mb-3" style="width: 336px;">
                    <label for="password">생년월일</label> 
                    <input type="date" class="form-control" id="password" placeholder="" value="" required name="user-password">

                </div>

                <div class="mb-3">
                    <label for="firstName">성별</label> 
                    <br>
                    <input type="radio" v-model="gender" id="gender1" value="M" checked="checked">
                            <label for="gender1">남</label>&nbsp;
  <input type="radio" v-model="gender" id="gender2" value="W">
                            <label for="gender2" >여</label>

                </div>

                <div class="mb-3" style="width: 336px;">
                    <label for="email">키</label>
                    <input type="email"  v-model="height" class="form-control" id="email" placeholder="키를 입력하세요" name="user-email" cm>
                    
                </div>
                <div class="mb-3" style="width: 336px;">
                    <label for="email">몸무게</label>
                    <input type="email" class="form-control" v-model="weight" id="email" placeholder="몸무게를 입력하세요" name="user-email">
                </div>

                <div class="mb-3"> 
                    <label for="address">주소</label> 

                    <button @click="execDaumPostcode()">주소 찾기</button> 
                    <input type="text" class="form-control" v-model="zipcode" style="width: 250px;" name="zipcode" placeholder = "우편번호" readonly />
                    
                    <input type="text" class="form-control" v-model="address" name="address" placeholder = "도로명주소" readonly />
                    <input type="text" v-model="detailedAddress" name="detailedAddress" placeholder = "상세주소" class="form-control"/>
                </div>
                <div class="mb-3" style="width: 336px;">
                    <label for="email">장기요양등급</label>
                   
        <v-select
        v-model="longTermCareGrade"
          :items="items"
          label="Standard"
          item-text="name"
        item-value="value"
        ></v-select>  
                </div>
                <div class="mb-3">
                    <label for="email">특이사항</label>
                    <v-col
        cols="12"
        md="6"
      >
        <v-textarea v-model="comment"
          solo
          name="input-7-4"
          label="Solo textarea"
        ></v-textarea>
      </v-col>   
                </div>
                <div class="mb-3">
                    <label for="firstName">반려동물유무</label> 
                    <br>
                    <input type="radio" v-model="pet" id="O" value="0" checked="checked">
                            <label for="O">O</label>&nbsp;
                        <input type="radio" v-model="pet" id="X" value="1">
                            <label for="X">X</label>

                </div>
                <div class="mb-3">
                    <label for="firstName">cctv 유무</label> 
                    <br>
                    <input type="radio" v-model="isCctvAgreement" id="O1" value="0" checked="checked">
                            <label for="O1">O</label>&nbsp;
                        <input type="radio" v-model="isCctvAgreement" id="X1" value="1">
                            <label for="X1">X</label>

                </div>
                <div class="mb-3">
                  <label for="firstName">케어유형</label> <br>
     <input type="radio" v-model="careType" id="oldman" value="oldman" checked="checked">
                            <label for="oldman">노인</label>&nbsp;
                        <input type="radio" v-model="careType" id="child" value="child">
                            <label for="child">아동</label>&nbsp;
                        <input type="radio" v-model="careType" id="pregnantwomen" value="pregnantwomen">
                            <label for="pregnantwomen">임산부</label>&nbsp;
                        <input type="radio" v-model="careType" id="patient" value="patient">
                            <label for="patient">환자</label>
                </div>
<div class="mb-3">
  <label for="firstName">코로나검사여부</label> <br>
                
<input type="radio" v-model="coronaTest" id="O2" value="0" checked="checked ">
                            <label for="O2">O</label>&nbsp;
                        <input type="radio" v-model="coronaTest" id="X2" value="1">
                            <label for="X2">X</label>
</div>
<div class="mb-3">
  <label for="firstName">이미지 업로드</label> <br>
 <v-file-input type="file" v-model="attachFiles" name="attachFiles" id="attachFiles" multiple="multiple"></v-file-input>
 </div>
                <hr class="mb-4">
                <v-btn class="ma-2" outlined color="indigo" id="clickme" @click="clickme">등록</v-btn>
                <v-btn class="ma-2" outlined color="indigo" id="clickme" @click="back">돌아가기</v-btn>
                <hr class="mb-4">

                <footer th:replace="/fragments/semantic :: footer"></footer>

        </div>

    </div>

</body>
  
</template>

<script>



export default {
    
data(){
    return{
        avatar:'',
        name: '',
        gender: '',
        birth: (new Date(Date.now() - (new Date()).getTimezoneOffset() * 60000)).toISOString().substr(0, 10),
        height:'',
        weight:'',
        zipcode:'',
        address:'',
        detailedAddress:'',
        longTermCareGrade:['1','2','3'],
        comment:'',
        pet:'',
        isCctvAgreement:'',
        careType:'',
        coronaTest:'',
        attachFiles:'',
        items:[
          {name:'없음',value:'0'},
          {name:'1',value:'1'},
      {name:'2',value:'2'},
      {name:'3',value:'3'},
        ]
    }
},
methods:{  
execDaumPostcode() {
      new window.daum.Postcode({
        oncomplete: (data) => {
          if (this.extraAddress !== "") {
            this.extraAddress = "";
          }
          if (data.userSelectedType === "R") {
            // 사용자가 도로명 주소를 선택했을 경우
            this.address = data.roadAddress;
          } else {
            // 사용자가 지번 주소를 선택했을 경우(J)
            this.address = data.jibunAddress;
          }
 
          // 사용자가 선택한 주소가 도로명 타입일때 참고항목을 조합한다.
          if (data.userSelectedType === "R") {
            // 법정동명이 있을 경우 추가한다. (법정리는 제외)
            // 법정동의 경우 마지막 문자가 "동/로/가"로 끝난다.
            if (data.bname !== "" && /[동|로|가]$/g.test(data.bname)) {
              this.extraAddress += data.bname;
            }
            // 건물명이 있고, 공동주택일 경우 추가한다.
            if (data.buildingName !== "" && data.apartment === "Y") {
              this.extraAddress +=
                this.extraAddress !== ""
                  ? `, ${data.buildingName}`
                  : data.buildingName;
            }
            // 표시할 참고항목이 있을 경우, 괄호까지 추가한 최종 문자열을 만든다.
            if (this.extraAddress !== "") {
              this.extraAddress = `(${this.extraAddress})`;
            }
          } else {
            this.extraAddress = "";
          }
          // 우편번호를 입력한다.
          this.zipcode = data.zonecode;
        },
      }).open();
    },
  
        changeImage(e){
        var file = e.target.files[0]
        var reader = new FileReader()
        var that = this
        reader.readAsDataURL(file)
        reader.onload = function(){
            that.avatar = this.result
        }
    },
     back() {
            this.$router.push({
        path:'/carenote/caretargets'
    })
  },
    clickme(){ 
      
        let formData = new FormData() 
                
                formData.append('name',this.name);
                formData.append('gender',this.gender);
                formData.append('birth',this.birth);
                formData.append('height',this.height);
                formData.append('weight',this.weight);
                formData.append('zipcode',this.zipcode);
                formData.append('address',this.address);
                formData.append('detailedAddress',this.detailedAddress);
                formData.append('longTermCareGrade',this.longTermCareGrade);
                formData.append('comment',this.comment);
                formData.append('pet',this.pet);
                formData.append('isCctvAgreement',this.isCctvAgreement);
                formData.append('careType',this.careType);
                formData.append('coronaTest',this.coronaTest);
                

                for (let i = 0; i < this.attachFiles.length; i++) {
                formData.append('attachFiles', this.attachFiles[i]);
                }
                // console.log(formData);
    this.$http
    .post('/api/dashboard/caretargets/new',formData, {
    withCredentials: true
    
    })
    
     .then(res => {
      console.log(res);
    })
      .catch(err => {
       console.log(err);
    }); 
    alert('대상인이 등록 되었습니다.')
                
       this.$router.push({ path: '/carenote/caretargets' })
       location.reload();
    
        },        
        
    },
}

</script>

<style scoped lang="scss">



.contents {
  display: flex;
  flex-direction: row;
  margin-top: 30px;
}
.contents .upload-box {
  width: 100%;
  margin-right: 30px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.contents .upload-box .drag-file {
  position: relative;
  width: 100%;
  height: 360px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border: 3px dashed #dbdbdb;
}
.contents .upload-box .drag-file.highlight {
  border: 3px dashed red;
}
.contents .upload-box .drag-file .image {
  width: 40px;
}
.contents .upload-box .drag-file .message {
  margin-bottom: 0;
}
.contents .upload-box .drag-file .preview {
  display: none;
  position: absolute;
  left: 0;
  height: 0;
  width: 100%;
  height: 100%;
}
.contents .upload-box .file-label {
  margin-top: 30px;
  background-color: #81C784;
  color: #fff;
  text-align: center;
  padding: 10px 0;
  width: 65%;
  border-radius: 6px;
  cursor: pointer;
}
.contents .upload-box .file {
  display: none;
}

@media (max-width: 700px) {
  .contents {
    display: flex;
    flex-direction: column;
    margin-top: 30px;
  }
  .contents .upload-box {
    width: 100%;
    box-sizing: border-box;
    margin-right: 0;
  }
  .contents .upload-box .drag-file {
    height: 150px;
  }
  .contents .files {
    width: 100%;
    box-sizing: border-box;
    margin-right: 0;
    overflow: initial;
  }
}
        

.box{width: 450px; height: 45px; border: 1px solid #666; padding: 10px;}
.box1{width: 250px; height: 45px; border: 1px solid #666; padding: 10px;}
.pbox{width: 120px; height: 45px; border: 1px solid #666; padding: 10px;}


ul{
    list-style: none;
}
    .content{
        width:100%;
        min-height: 800px;
        overflow: hidden;
    }
    .content .join{
        width:100%;
        max-width: 800px;
        margin: 50px auto 150px auto;
        position: relative;
        text-align: left;
        box-sizing: border-box;
        padding: 0 15px 0 15px;
    }
    .content .join .div_join{
        width: 100%;
        position: relative;
        box-sizing: border-box;
        text-align: center;
        background-color: #ffffff;
        border: 0;
        box-shadow: 0 0 18px #d3d3d3;
        border-radius: 10px;
        padding: 40px 10px 40px 10px;
    }
    .content1{
        text-align: left;
        display: block;
        
        
    }
    .content1 span{
        font-size: 20px;
        
    }
    .content1 input[type="text"],
    input[type="number"]{
        border-radius: 5px;
        border: 1px #e3e3e3 solid;
        border: 1px solid #666;
    }
    .data_form{
        border: 2px black solid;
        border-radius: 3;
    }
    .submit{
        text-align: center;
        
    }
    .information{
        width: 700px;
        height: 150px;
        border: 2px #e3e3e3 double;
    }
    .input_form_number{
        text-align: right;
    }
    

input[type=radio]{
	width: 0;
  height: 0;
  position: absolute;
  left: -9999px;
  
}
input[type=radio] + label{
  line-height: 50px;
  width: 50px;
  height: 50px;
  
  box-sizing: border-box;
  position: relative;
  display: inline-block;
  border: solid 1px #DDD;
  background-color: #FFF;
  
  text-align: center;
  box-shadow: 0 0 0 rgba(255, 255, 255, 0);
  transition: border-color .15s ease-out,  color .25s ease-out,  background-color .15s ease-out, box-shadow .15s ease-out;
  cursor: pointer;
  border-radius: 100%;
}
input[type=radio]:checked + label{
	background-color: #81C784;
  color: #FFF;
  
  border-color: #81C784;
  z-index: 1;
}
button {
    color: #444444;
    background: #F3F3F3;
    border: 1px #DADADA solid;
    padding: 5px 10px;
    border-radius: 2px;
    font-weight: bold;
    font-size: 9pt;
    outline: none;
}

button:hover {
    border: 1px #C6C6C6 solid;
    box-shadow: 1px 1px 1px #EAEAEA;
    color: #333333;
    background: #F7F7F7;
}

button:active {
    box-shadow: inset 1px 1px 1px #DFDFDF;   
}




















    
</style>