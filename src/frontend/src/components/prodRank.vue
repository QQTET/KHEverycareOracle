<template>
<v-row>
	<p class="fs-4 mt-10 ml-15">HOT LIST</p>
    <div class="mt-4 scale ranking col" v-for="item in storeRank" :key="item.index" @click="detail(item)">
	<img :src="'https://localhost:8080/api/images/'+item.storeFileName" 
  class="rounded-circle mx-auto d-block" width="140" 
  height="140" />
        <div class="text-center mt-4">
		<b>{{item.name}}</b>
		</div>
    </div>
    
</v-row>  

</template>

<script>
export default {
props:{
    storeRank:{
        required:true
    }
},
methods:{
   detail(item){
      this.$emit('detail',item.id);
  }
 }
}
</script>

<style>

</style>