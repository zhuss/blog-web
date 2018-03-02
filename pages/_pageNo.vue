<template>
  <section class="container">
      <div class="list">
          <div class="item" v-for="item in blogRows" :key="item.id" @click="itemClick(item.id)">
              <h2 class="item-title">{{item.title}}</h2>
              <p class="item-author"><span class="author">文 / {{item.author}}</span><span class="date">{{moment(item.createdAt).format('YYYY / MM / DD')}}</span></p>
              <p class="item-abstract">{{item.abstract}}</p>
          </div>
      </div>
      <div class="page">
         <button class="btn" :disabled="pageNo <= 1" @click="prvePageBtnClick()">上一页</button>
         <span class="page-num">{{pageNo}}</span>
         <button class="btn" :disabled="pageNo*pageCount >= blogCount" @click="nextPageBtnClick()">下一页</button>
      </div>
  </section>
</template>

<script>
//import AppLogo from '~/components/AppLogo.vue'
import axios from 'axios'
import moment from 'moment'

export default {
  // components: {
  //   AppLogo
  // },
  async asyncData({params,error}){
    let pageNo = 1;
    if(params.pageNo&&params.pageNo>0) pageNo = params.pageNo;
    let {data} = await axios.get('http://47.100.55.91:3000/blog/list',{params:{pageNo:pageNo}});
    if(data.code == 200){
      return {
         blogRows:data.data.rows,
         blogCount:data.data.count,
         pageNo:pageNo
      };
    }else{
      error({ statusCode: data.code, message:data.msg});
    }
  },
  data(){
    return {
       pageCount:10,
       moment:moment
    }
  },
  methods:{
    //点击item
    itemClick(id){
      this.$router.push({
          path:"/blog/"+id
      });
    },
    //下页
    nextPageBtnClick(){
       let pageNo = ++this.pageNo;
       this.$router.push({
           path:"/"+pageNo
       });
    },
    //上页
    prvePageBtnClick(){
      let pageNo  = --this.pageNo;
      this.$router.push({
           path:"/"+pageNo
       });
    }
  }
}
</script>
<style scoped>
::-webkit-scrollbar{
  width: 0;
  height: 0;
}
.container {
  padding-bottom: 30px;
  width: 100%;
  max-width: 800px;
  height: auto;
  margin-left:auto; 
}
.list{
  width: 100%;
  height: auto;
}
.list .item{
  margin: 10px 0;
  padding: 30px;
  background: #FFF;
  transition: all .3s ease-in-out;
  cursor: pointer;
}
.list .item:hover{
  box-shadow: 0 2px 6px rgba(0,0,0,.5);
  transform: translateX(-5px);
}

.item-title{
  font-weight: bold;
  margin-bottom: 10px;
}
.item-author{
  font-size: 14px;
  color: #333;
  display: flex;
}
.item .author{
   flex: 1;
}
.item .date{
  padding-bottom: 10px;
  border-bottom: 2px solid #CCC;
}
.item-abstract{
  font-size: 16px;
  margin-top: 10px;
}
.page{
  width: 100%;
  height: 40px;
  display: flex;
  background: #FFF;
}
.page .btn{
  flex: 1;
  padding: 0;
  height: 40px;
  border: none;
  box-sizing: border-box;
  background: transparent;
  outline: none;
  cursor: pointer;
}
.page .page-num{
  flex: 1;
  height: 40px;
  line-height: 40px;
  text-align: center;
}
</style>
