<template>
<div class="layout">
    <Layout>
        <router-link :to="{path:'/'}"><Header></Header></router-link>
        <Layout>
            <Content class="content">
                <Row>
                    <Col :xl="16" :xs="13">
                        <Row>
                            <Col :xl="{span:5,offset:0}" :xs="{span:11,offset:0}"><span>书籍热评榜</span></Col>
                            <Col :xl="{span:2,offset:17}" :xs="{span:3,offset:8}">
                                <Button size='small' type="text" @click="OutputMore" v-show="show">更多</Button>
                                <Button size='small' type="text" v-show="!show" @click="back">返回</Button>
                            </Col>
                        </Row>
                        <hr/>
                        <MyBookList :content='books' :num='more' v-show='show' @acceptfromchild='showId'></MyBookList>
                        <MyBookDetail v-show='!show' :site='bookDetail' :star='bookDetail.grade/2'></MyBookDetail>
                    </Col>
                    <Col :xl="{span:7,offset:1}" :xs="{span:10,offset:1}">
                        <span class='title'>书籍排行榜</span>
                        <hr/>
                        <MyBookCharts :content='books'></MyBookCharts>
                    </Col>
                </Row>
            </Content>
        </Layout>
    </Layout>
</div>
</template>
<script>
import MyHeader from '../components/MyHeader'
import MyBookList from '../components/MyBookList'
import MyBookCharts from '../components/MyBookCharts'
import MyBookDetail from '../components/MyBookDetail'
import Axios from 'axios'
export default {
  name: 'Book',
  components: {
    MyBookList: MyBookList,
    Header: MyHeader,
    MyBookCharts: MyBookCharts,
    MyBookDetail
  },
  data () {
    return {
      books: [

      ],
      more: 4,
      moreback: '更多',
      show: true,
      bookDetail: [

      ]
    }
  },
  methods: {
    OutputMore () {
      const msg = this.$Message.loading({
        content: 'Loading...',
        duration: 0
      })
      setTimeout(msg, 3000)
      setTimeout(() => {
        this.more = 0
      }, 3000)
    },
    getData () {
      Axios.get('api/book/topBook').then((book) => {
        this.books = book.data
        console.log(book.data)
      })
    },
    showId (value) {
      console.log(value)
      Axios.get('api/book/get/' + value).then((bookDetail) => {
        this.bookDetail = bookDetail.data
        this.show = false
        this.moreback = '返回'
        console.log(this.bookDetail)
      })
    },
    back () {
      this.show = true
    }
  },
  created () {
    this.getData()
  }
}
</script>
<style scoped>
.content{
    padding:1em 0.5rem 0 1rem;
    background-color: #fff;
}
.content hr{
    padding: 0;
    margin-top:0.2rem;
}
.title{
  font-size: .23rem;
  line-height:.2rem
}
</style>
