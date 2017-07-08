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
    data(){
      return {books:[
        {bookName:'武侠小说',bookPrice:30,bookCover:'https://ss2.baidu.com/6ONYsjip0QIZ8tyhnq/it/u=2073765524,865271981&fm=58',id:1},
        {bookName:'言情小说',bookPrice:40,bookCover:'https://ss0.baidu.com/6ONWsjip0QIZ8tyhnq/it/u=248685597,3438291033&fm=58',id:2},
      ]}
    },
    components:{},
    methods:{}
  }
</script>

