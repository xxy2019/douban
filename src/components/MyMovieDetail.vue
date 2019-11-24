<template>
    <Row>
      <Row class="title">
        <Col :xl="16" :xs="24" class="enum_list">
          <h3 class="title">{{site.name}}</h3>
              <Col :xl="6" :xs="5">
                <img :src="'https://images.weserv.nl/?url='+site.coverUrl"  id="m_pic">
              </Col>
              <Col :xl="{span:15,offset:3}" :xs="{span:16,offset:2}" class="detail">
                <p v-if='site.director'>
                  <span class="d_title">导演：</span>{{''+site.director}}</p>
                <p v-if='site.screenwriter'>
                  <span class="d_title">编剧：</span>{{''+site.screenwriter.substring(0,20)}}
                </p>
                <p v-if='site.starring'>
                  <span class="d_title">主演: </span>{{''+site.starring.substring(0,20)}}
                </p>
                <p v-if='site.type'>
                <span class="d_title">类型: </span>{{''+site.type}}
                </p>
                <p v-if='site.countriesRegions'>
                <span class="d_title">制片国家/地区: </span>{{''+site.countriesRegions}}
                </p>
                <p v-if='site.language'>
                <span class="d_title">语言: </span>{{''+site.language}}
                </p>
                <p v-if='site.date'>
                <span class="d_title">首播: </span>{{''+site.date}}
                </p>
                <p v-if='site.length'>
                <span class="d_title">片长: </span>{{''+site.length}}
                </p>
                <p v-if='site.otherName'>
                  <span class="d_title">又名：</span>{{''+site.otherName.substring(0,20)}}
                </p>
                <p>
                 <span class="d_title">IMDb链接: </span> {{' '+site.imDb}}
                </p>
              </Col>
        </Col>
          <Col :xl="{span:8}"  class="p_right" :xs="24">
              <p>豆瓣评分</p>
              <Rate show-text allow-half v-model="star" disabled>
                <span style="color: #f5a623">{{star*2}}</span>
              </Rate>
              <p>{{site.scoreNumber+"评价"}}</p>
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
  name: 'MyMovieDetail',
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
