<template>
  <section class="container">
       <div class="blog">
         <h1>{{title}}</h1>
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
  }
}
</script>
<style scoped>
.container{
  padding-bottom: 30px;
  width: 100%;
  max-width: 800px;
  height: auto;
  margin-left:auto;
}
.blog{
  padding: 30px;
  background: #FFF;
  min-height: 100%;
}
</style>


