<template>
  <div>
    <div class="col-md-3">
      <div class="panel panel-warning">
        <div class="panel-heading">
          书名:<span v-show="!flag">{{book.bookName}}</span>
          <input type="text" v-model="book.bookName" v-show="flag">
        </div>
        <div class="panel-body text-center">
          <img :src="book.bookCover" alt="">
        </div>
        <div class="panel-footer">
          价格:<span v-show="!flag">{{book.bookPrice | currency('￥')}}</span>
          <input type="text" v-model="book.bookPrice" v-show="flag">
          <button type="button" class="btn btn-warning btn-xs" @click="changeFlag" v-show="!flag">修改</button>
          <button type="button" class="btn btn-primary btn-xs" v-show="flag" @click="update">确认修改</button>
          <button type="button" class="btn btn-danger btn-xs" @click="remove" v-show="!flag">删除</button>
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
      //页面一加载获取id对应的数据
      this.id=this.$route.params.id;
      this.$http.get('/book?id='+this.id).then(res=>{
          this.book=res.body;
      })
    },
    data(){
      return {
        book:{
          bookName:'',
          bookPrice:'',
          bookCover:''
        },
        id:'',
        flag:false//默认不显示输入框
      }
    },
    components:{},
    methods:{
        changeFlag(){
            this.flag=!this.flag;
        },
        update(){
            //服务器调用res.end就会触发then中的成功的回调
            this.$http.put('/book?id='+this.id,this.book).then(()=>{
                this.flag=false;//VueResource将then中的this处理掉了，默认指向的是当前组件
            })
        },
        remove(){
           this.$http.delete('/book?id='+this.id).then(()=>{
               this.$router.push('/list');
           })

        }
    }
  }
</script>

