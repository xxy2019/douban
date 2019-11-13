<template>
<div class="layout">
    <Layout>
        <Header>Header</Header>
        <Layout>
            <Content>
                <Row class="l_content">
                    <Col span="7" offset="1">
                        <h4 class="m_t">电影</h4>
                        <span class="more"><router-link :to="{path:'/Movie'}" style="color:#000;text-decoration: none;">更多</router-link></span>
                        <div class="clear"></div>
                        <MyText></MyText>
                    </Col>
                    <Col span="7" offset="1">
                        <h4 class="m_t">音乐</h4>
                        <span class="more"><router-link :to="{path:'/Music'}" style="color:#000;text-decoration: none;">更多</router-link></span>
                        <div class="clear"></div>
                        <MyText></MyText>
                    </Col>
                    <Col span="7" offset="1">
                        <h4 class="m_t">书籍</h4>
                        <span class="more"><router-link :to="{path:'/Book'}" style="color:#000;text-decoration: none;">更多</router-link></span>
                        <div class="clear"></div>
                        <MyText></MyText>
                    </Col>
                </row>
            </Content>
        </Layout>
    </Layout>
</div>
</template>
<script>
import MyHeader from '../components/MyHeader'
import MyText from '../components/MyText'
export default {
    name:'Home',
    components:{
        Header:MyHeader,
        MyText:MyText,
    },
    data(){
        return{
        }
    },
    methods:{
    },
    created () {
    this.$http.get('/api/book/get').then(response => {
      console.log(response.body)
    }, reponse => {

    })
  }
}
</script>
<style lang="css" scoped>
.l_content{
  width:75rem;
  height:45.625rem;
  margin-left: 1.875rem;
}
.m_t{
  height:2.8125rem;
  width:4.125rem;
  line-height:2.8125rem;
  margin: 0rem;
  text-align: center;
  float:left;
}
.more{
  width:4.5625rem;
  height:2.8125rem;
  display: block;
  line-height:2.8125rem;
  text-align: center;
  float:right;
}
.clear{
  clear: both;
  width:20rem;
  height:.4375rem;
  border-top:.0625rem solid #555;
  margin-left: .6rem;
}
</style>