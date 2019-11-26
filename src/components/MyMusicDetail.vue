<template>
    <Row>
      <Row>
        <Col :xl="16" :xs="{span:24}">
         <Row>
            <li class="enum_list">
              <h2 class="title">{{site.name}}</h2>
              <Col :xl="5" :xs="8">
                <img :src="'https://images.weserv.nl/?url='+site.coverUrl"  id="m_pic">
              </Col>
              <Col :xl="{span:14,offset:5}" :xs="{span:13,offset:3}">
                <div class="detail">
                  <p v-if='site.singer'><span class="d_title">表演者：</span>{{' '+site.singer}}</p>
                  <p v-if='site.style'>
                    <span class="d_title">流派：</span>{{' '+site.style}}
                  </p>
                  <p v-if='site.albumType'>
                    <span class="d_title">专辑类型: </span>{{' '+site.albumType}}
                  </p>
                  <p v-if='site.medium'>
                    <span class="d_title">介质: </span>{{' '+site.medium}}
                  </p>
                  <p v-if='site.issueDate'>
                    <span class="d_title">发行时间:</span>{{' '+site.issueDate.substring(0,10)}}
                  </p>
                  <p v-if='site.publisher'>
                    <span class="d_title">出版者:</span>{{' '+site.publisher}}
                  </p>
                  <p v-if='site.songNumbers'>
                    <span class="d_title">唱片数:</span>{{' '+site.songNumbers}}
                  </p>
                  <p v-if="site.barcode==Null">
                    <span class="d_title">条形码:</span>{{' '+site.barcode}}
                  </p>
                  <p v-if="site.otherVersion==Null">
                    <span class="d_title">其他版本:</span>{{' '+site.otherVersion}}
                  </p>
                </div>
              </Col>
            </li>
          </Row>
        </Col>
        <Col :xl="{span:8}"  class="p_right" :xs="24">
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
      valueCustomText: 0,
      gotop: true
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
<style lang="css" scoped>
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
.enum_list{
  height:4.5rem;
  margin-top: 0.225rem;
  margin-left: 0.625rem;
}
#m_pic{
  width:116px;
  height: 134px;
  margin-right:0.2rem;
  float:left;
  margin-top:.225rem;
}
.detail{
  height:130px;
}
.detail p{
  font-size: 0.1rem;
  margin: .0325rem;
}
.p_right{
  margin:1.5rem 0 0.5rem;
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
  line-height:24px;
  margin-bottom: 20px;
}
</style>
