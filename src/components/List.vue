<template>
  <div>
     <div class="col-md-3" v-for="book in books">
       <div class="panel panel-warning">
         <div class="panel-heading">
           书名:{{book.bookName}}
         </div>
         <div class="panel-body text-center">
           <img :src="book.bookCover" alt="">
         </div>
         <div class="panel-footer">
           价格:{{book.bookPrice | currency('￥')}}
           <router-link :to="{name:'detail',params:{id:book.id}}">进入详情</router-link>
         </div>
       </div>
     </div>
  </div>
</template>
<style scoped>
    img{
      width: 100px;
      height: 150px;
    }
</style>
<script>
  export default{
    filters:{
       currency(input,params1){
           return params1+input;
       }
    },
    created(){
        //在config目录中的index.js中的proxyTable中 配置代理表
       this.$http.get('/book').then((res)=>{
           this.books=res.body;
       })
    },
    data(){
      return {books:[]}
    },
    components:{},
    methods:{}
  }
</script>

