<template>
    <div>
        <v-card flat>
    <v-card-text>
      <v-container fluid>
        <v-row class="mt-5">
            <v-text-field
            v-model="title"
            placeholder="제목을 입력하세요"
            outlined
          ></v-text-field>
        </v-row>
          <v-row>
              <v-textarea
              v-model="comment"
              label="내용을 입력하세요"
              outlined
            >
            </v-textarea>
          </v-row>
      </v-container>
      <v-card-actions v-if="$store.state.userStore.id==='admin'">
        <v-btn
          text
          @click="edit"
          color="primary">
          수정
        </v-btn>
        <v-btn
          text
          color="error"
          @click="drop">
          삭제
        </v-btn>
        <v-btn
          text
          @click="back">
          취소
        </v-btn>
        
      </v-card-actions>
      </v-card-text>
  </v-card>  
    </div>
</template>

<script>
export default {
mounted() {
     const id = Number(this.$route.params.contentId);
    this.$http
    .get(`/api/faq/${id}`,{
        withCredentials:true
      })
	.then((res)=>{
        console.log(res.data);
        this.title=res.data.body.title,
        this.comment=res.data.body.content
        this.id=res.data.body.id
      }).catch(err =>{
				alert(err);
				console.log(err);
			})
},
data(){
    return{
        id: this.id,
        title: this.title,
        comment: this.comment
    }
},
methods:{
    edit(){
    var formData = new FormData();
    formData.append('id', this.id);
    formData.append('title', this.title);
    formData.append('content', this.comment);
    this.$http
    .patch(`/api/admin/faq`, formData, {
    withCredentials: true
    })
     .then(res => {
      console.log(res);
    })
      .catch(err => {
       console.log(err);
    });
  },
  drop(){
    var Id = {
           id:this.id,
           }
    this.$http
    .delete(`/api/admin/faq/${this.id}`, {
      withCredentials: true
    })
    .then((res)=> {
      console.log(res)
    }).catch((err)=>{
      console.log(err)
    })
  },
back(){
    this.$router.push({
        path:'/faq'
    })
}
}
}
</script>

<style>

</style>