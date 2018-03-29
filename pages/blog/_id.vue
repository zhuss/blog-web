<template>
  <section class="container">
       <div class="blog">
         <h1 class="title">{{title}}</h1>
         <p class="author">文 / {{author}}  {{moment(createdAt).format('YYYY / MM / DD')}}</p>
         <div class="abstract">{{abstract}}</div>
         <div class="content" v-html="content"></div>
       </div>
  </section>
</template>
<script>
import axios from 'axios'
import moment from 'moment'
export default {
  async asyncData({params,error}){
    let id = params.id;
    let {data} = await axios.get('http://47.100.55.91:3000/blog/get',{params:{id:id}});
    if(data.code == 200){
        return data.data;
    }else{
      error({ statusCode: data.code, message:data.msg});
    }
  },
  data(){
    return {
       moment:moment
    }
  }
}
</script>
<style>
.blog .content p,.blog .content div{
  margin: 15px 0;
}
.blog .content img{
  max-width: 100%;
  display: inline-block;
  margin: 0 auto;
}
</style>
<style scoped>
.container{
  width: 100%;
  max-width: 800px;
  height: auto;
  min-height: 100%;
  margin-left:auto;
}
.blog{
  padding: 30px;
  background: #FFF;
  min-height: 100%;
}
.blog .title{
  font-size: 20px;
  margin: 10px 0;
}
.blog .author{
  margin:20px 0;
}
.blog .abstract{
  font-size: 14px;
  color: #333;
  border: 1px solid #E6E6E6;
  padding: 20px;
  background: #EEE;
}
.blog .content{
  padding: 20px 0;
}
</style>


