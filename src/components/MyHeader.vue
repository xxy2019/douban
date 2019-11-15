<template>
    <div class="headertext">
     <div class="logo">
       <img src="../assets/logo.png">
     </div>
     <div class="title">
       <span>豆瓣内容偏好榜单</span>
     </div>
  </div>
</template>
<script>
export default {
    name:'MyHeader'
}
</script>
<style lang="css" scoped>
.headertext{
  background-image:url(../assets/background_color.png);
  background-size: 100%,100%;
  color:#fff;
}
.logo{
  width:13.5625rem;
  height: 2.375rem;
  position: relative;
  top:2rem;
  left:2rem;
}
.title{
  width: 100%;
  height: 7rem;
  text-align: right;
}
.title span{
  color:#fff;
  font-size:1.8rem;
  position: relative;
  top: 2rem;
  left: -2rem;
  font-family: 'Courier New', Courier, monospace;
}
</style>