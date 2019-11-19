<template>
    <Row>
      <Row>
        <Col span="12">
        <li class="enum_list">
            <h3 id="title">{{site.name}}</h3>
            <img :src="'https://images.weserv.nl/?url='+site.coverUrl"  id="m_pic">
            <div class="detail">
              <p>{{'表演者：'+site.singer}}</p>
              <p>
                {{'流派：'+site.style}}
              </p>
              <p>
                {{'专辑类型: '+site.albumType}}
              </p>
              <p>
              {{'介质: '+site.medium}}
              </p>
              <p>
              {{'发行时间:'+site.issueDate.substring(0,10)}}
              </p>
              <p>
              {{'出版者:'+site.publisher}}
              </p>
              <p>
              {{'唱片数:'+site.songNumbers}}
              </p>
              <p>
              {{'条形码:'+site.barcode}}
              </p>
              <p v-if="site.otherVersion==NULL">
              {{'其他版本:'+site.otherVersion}}
              </p>
            </div>
          </li>
        </Col>
        <Col span="8" offset="4"  class="p_right">
            <p>豆瓣评分</p>
            <Rate show-text allow-half v-model="star" disabled>
              <span style="color: #f5a623">{{star*2}}</span>
            </Rate>
            <p>{{site.reviewNum+"评价"}}</p>
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
  name: 'MyMusicDetail',
  data () {
    return {
      valueCustomText: 0
    }
  },
  props: ['site', 'star']
}
</script>
<style lang="css">
.text{
  width:21.8rem;
  height:37.5rem;
  margin-left: 1.725rem;
  float:left;
}
ul,li{
  list-style: none;
}
.enum_list{
  width:21.875rem;
  height:12.5rem;
  margin-top: 0.625rem;
  margin-left: 0.625rem;
}
#m_pic{
  width:8.4375rem;
  height:8.4375rem;
  float:left;
  margin-top:.625rem;
}
.detail{
  width:10rem;
  height:10rem;
  margin-left: .9375rem;
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
  margin-top: 40px;
  border-top: 1px solid #eee;
}
.intro_title{
  font-weight: bold;
  font-size: 1.25rem;
  margin: 2px;
}
.intro_content{
  font-size:.875rem;
  text-indent:2rem;
  line-height:1.875rem;
}
</style>
