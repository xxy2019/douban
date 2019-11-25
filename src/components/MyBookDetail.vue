<template>
    <Row>
      <Row>
        <Col :xl="16" :xs="24">
          <Row class="enum_list">
            <h3 class="title">{{site.name}}</h3>
            <Col :xl="5" :xs="5">
            <img :src="'https://images.weserv.nl/?url='+site.cover"  id="m_pic">
            </Col>
            <Col :xl="{span:13,offset:6}" :xs="{span:16,offset:2}">
            <div class="detail">
              <p v-if='site.author'>
                <span class="d_title">作者：</span>{{''+site.author}}</p>
              <p v-if='site.press'>
                <span class="d_title">出版社：</span>{{''+site.press}}
              </p>
              <p v-if='site.originalName'>
                <span class="d_title">原作名: </span>{{''+site.originalName}}
              </p>
              <p v-if='site.translator'>
              <span class="d_title">译者: </span>{{''+site.translator}}
              </p>
              <p v-if='site.year'>
              <span class="d_title">出版年: </span>{{''+site.year}}
              </p>
              <p v-if='site.pages'>
              <span class="d_title">页数: </span>{{''+site.pages}}
              </p>
              <p v-if='site.number'>
              <span class="d_title">定价: </span>{{''+site.number}}
              </p>
              <p v-if='site.binding'>
              <span class="d_title">装帧: </span>{{''+site.binding}}
              </p>
              <p v-if='site.isbn'>
                <span class="d_title">ISBN：</span>{{''+site.isbn}}
              </p>
            </div>
            </Col>
          </Row>
        </Col>
        <Col :xl="{span:8}"  class="p_right" :xs="24">
            <p>豆瓣评分</p>
            <Rate show-text allow-half v-model="star" disabled>
              <span style="color: #f5a623">{{star*2}}</span>
            </Rate>
            <p>{{site.number+"评价"}}</p>
        </Col>
        </Row>
        <Row class="b_introduction">
         <p class="intro_title">简介</p>
         <p class="intro_content">{{site.introduction}}</p>
        </Row>
    </Row>
</template>
<script>
export default {
  name: 'MyBookDetail',
  data () {
    return {
    }
  },
  props: ['site', 'star']
}
</script>
<style lang="css">
.text{
  margin-left: 0.2rem;
}
.title{
  font-size: 0.3rem;
}
.d_title{
  font-size: 0.3rem;
  font-weight:bold;
}
ul,li{
  list-style: none;
}
#m_pic{
  width:2rem;
  height:2.3rem;
  float:left;
  margin-top:.225rem;
}
.detail p{
  font-size: 0.3rem;
  margin: .0325rem;
}
.p_right{
  margin:.75rem 0 0.2rem;
  border-left: .0125rem solid #aaa;
  padding-left:.625rem;
}
.b_introduction{
  border-top: .0125rem solid #aaa;
}
.intro_title{
  font-weight: bold;
  font-size: 0.3rem;
  margin: .1rem;
}
.intro_content{
  font-size:.3rem;
  text-indent:.6rem;
  line-height:.775rem;
}
</style>
