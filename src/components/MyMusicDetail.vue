<template>
    <Row>
      <Row>
        <Col span="12" :xs="24" :sm="12" :md="12" :lg="12">
         <Row>
           <li class="enum_list">
             <h2 id="title">{{site.name}}</h2>
              <Col span="12" :xs="24" :sm="12" :md="12" :lg="12">
                  <img :src="'https://images.weserv.nl/?url='+site.coverUrl"  id="m_pic">
              </Col>
            <Col span="12" :xs="24" :sm="12" :md="12" :lg="12">
            <Row class="detail">
              <Row><p v-if='site.singer'><span class="d_title">表演者：</span>{{' '+site.singer}}</p></Row>
              <Row><p v-if='site.style'>
                <span class="d_title">流派：</span>{{' '+site.style}}
              </p></Row>
              <Row><p v-if='site.albumType'>
                <span class="d_title">专辑类型: </span>{{' '+site.albumType}}
              </p></Row>
              <Row><p v-if='site.medium'>
              <span class="d_title">介质: </span>{{' '+site.medium}}
              </p></Row>
              <Row><p v-if='site.issueDate'>
              <span class="d_title">发行时间:</span>{{' '+site.issueDate.substring(0,10)}}
              </p></Row>
              <Row><p v-if='site.publisher'>
              <span class="d_title">出版者:</span>{{' '+site.publisher}}
              </p></Row>
              <Row><p v-if='site.songNumbers'>
              <span class="d_title">唱片数:</span>{{' '+site.songNumbers}}
              </p></Row>
              <Row><p v-if="site.barcode==Null">
              <span class="d_title">条形码:</span>{{' '+site.barcode}}
              </p></Row>
              <Row><p v-if="site.otherVersion==Null">
              <span class="d_title">其他版本:</span>{{' '+site.otherVersion}}
              </p></Row>
            </Row>
            </Col>
          </li>
          </Row>
        </Col>
        <Col span="8" offset="4"  class="p_right" :xs="24" :sm="8" :md="8" :lg="8">
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
        <Row class="b_introduction">
         <p class="intro_title">曲目</p>
         <p class="intro_content">{{site.track}}</p>
        </Row>
    </Row>
</template>
<script>
export default {
  name: 'MyMusicDetail',
  data () {
    return {
      valueCustomText: 0,
      gotop: true
    }
  },
  computed: {
    trackArray: function () {
      return this.site.track.split('0')
    }
  },
  props: ['site', 'star'],
  methods: {
    handleScroll () {
      let scrolltop = document.documentElement.scrollTop || document.body.scrollTop
      scrolltop > 30 ? (this.gotop = true) : (this.gotop = false)
    },
    toTop () {
      let top = document.documentElement.scrollTop || document.body.scrollTop
      const timeTop = setInterval(() => {
        document.body.scrollTop = document.documentElement.scrollTop = top -= 50
        if (top <= 0) {
          clearInterval(timeTop)
        }
      }, 10)
    }
  }
}
</script>
<style lang="css">
.text{
  width:21.8rem;
  height:37.5rem;
  margin-left: 1.725rem;
  float:left;
}
.d_title{
  font-size: 0.75rem;
  font-weight:bold;
}
ul,li{
  list-style: none;
}
.enum_list{
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
  margin-top: 2.5rem;
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
