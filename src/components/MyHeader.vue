<template>
    <div class="headertext">
        <Row>
            <Col :xs="{span:6}" :xl="{span:5,offset:1}" :md="{span:5,offset:1}" style="margin-top:.5rem">
                <img src="../assets/logo.png">
            </Col>
            <Col :xs="{span:16,offset:2}" :xl="{span:5,offset:13}" :md="{span:6,offset:12}" class="title">
                <span>豆瓣内容偏好榜单</span>
            </Col>
        </Row>
  </div>
</template>
<script>
export default {
  name: 'MyHeader'
}
</script>
<style lang="css" scoped>
.headertext{
  background-image:url(../assets/background_color.png);
  background-size: 100%,100%;
  color:#fff;
}
.headertext img{
  width: 150px;
}
.title{
  margin-top:100px;
  font-size: 28px;

}
.title span{
  color:#fff;
  font-family: 'Courier New', Courier, monospace;
}
</style>
