<template>
    <Row>
      <Row class="title">
        <Col span="16" class="enum_list">
          <h3 id="title">{{site.name}}</h3>
              <Col span="8" :xs="24" :lg="8">
                <img :src="'https://images.weserv.nl/?url='+site.coverUrl"  id="m_pic">
              </Col>
              <Col span="13" class="detail" offset="3" :xs="24" :lg="13">
                <p v-if='site.director'>{{'导演：'+site.director}}</p>
                <p v-if='site.screenwriter'>
                  {{'编剧：'+site.screenwriter.substring(0,20)}}
                </p>
                <p v-if='site.starring'>
                  {{'主演: '+site.starring.substring(0,20)}}
                </p>
                <p v-if='site.type'>
                {{'类型: '+site.type}}
                </p>
                <p v-if='site.countriesRegions'>
                {{'制片国家/地区:'+site.countriesRegions}}
                </p>
                <p v-if='site.language'>
                {{'语言:'+site.language}}
                </p>
                <p v-if='site.date'>
                {{'首播:'+site.date}}
                </p>
                <p v-if='site.length'>
                {{'片长:'+site.length}}
                </p>
                <p v-if='site.otherName'>
                  {{'又名：'+site.otherName.substring(0,20)}}
                </p>
                <p>
                  {{'IMDb链接: '+site.imDb}}
                </p>
              </Col>
        </Col>
          <Col span="8"  class="p_right" :xs="24" :lg="8">
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
.title{
}
ul,li{
  list-style: none;
}
.enum_list{
  margin-top: 0.625rem;
}
#m_pic{
  width:100%;
  height:100%;
  float:left;
  margin-top:.625rem;
}
.detail{
  float:right;
}
.detail p{
  font-size: 0.75rem;
  margin: .125rem;
}
.p_right{
  margin-top: 3.75rem;
  border-left: .0625rem solid #eee;
  padding-left:.625rem
}
.b_introduction{
  margin-top: 4.6875rem;
  border-top: .0625rem solid #eee;
}
.intro_title{
  font-weight: bold;
  font-size: 1.25rem;
  margin: .125rem;
}
.intro_content{
  font-size:.875rem;
  text-indent:2rem;
  line-height:1.875rem;
}
</style>
