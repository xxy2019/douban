<template>
    <div class="headertext">
        <Row>
            <Col :xs="{span:5,offset:1}" :xl="{span:5,offset:1}" :md="{span:5,offset:1}" style="margin-top:2rem">
                <img src="../assets/logo.png">
            </Col>
            <Col :xs="{span:15,offset:3}" :xl="{span:5,offset:13}" :md="{span:9,offset:9}" class="title">
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
  height: 9rem;
}
.title{
  margin-top:5rem;
  font-size: 1.8rem;

}
.title span{
  color:#fff;
  font-family: 'Courier New', Courier, monospace;
}
</style>
