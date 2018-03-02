<template>
  <div class="container">
      <div class="content">
        <h1>{{error.statusCode}}</h1>
        <p>{{error.message}}</p>
      </div>
  </div>
</template>
<script>
export default {
  props: ['error']
}
</script>
<style scoped>
.container{
    width: 100%;
    height: 100%;
}
.content{
    width: 400px;
    margin: 100px auto;
    background: #FFF;
    padding: 30px;
}
.content h1{
    text-align: center;
    font-size: 32px;
    margin-bottom:30px; 
    color: #999;
}
.content p{
    color: #999;
    text-align: center;
}
</style>


