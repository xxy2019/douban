<template>
<div class="layout">
    <Layout>
        <router-link :to="{path:'/'}"><Header></Header></router-link>
        <Layout>
            <Content class="content">
              <span class="book_button"  >近30日最受女性欢迎的书籍</span>
              <Button size="small" type="success" @click="OutputWomenLove">{{this.womensort.sort}}</Button>
                <Row>
                   <Col :xl="16" :xs="24">
                        <Row>
                            <Col :xl="{span:5,offset:0}" :xs="{span:11,offset:0}"><span class="title">书籍热评榜</span></Col>
                            <Col :xl="{span:2,offset:17}" :xs="{span:3,offset:8}">
                                <Button size='large' type="text" @click="OutputMore" v-show="show" v-if='Loveshow'>更多</Button>
                                <Button size='large' type="text" v-show="!show" @click="back">返回</Button>
                            </Col>
                        </Row>
                        <hr/>
                        <MyBookList :content='books' :num='more' v-show='show' v-if='Loveshow' @acceptfromchild='showId'></MyBookList>
                        <MyBookList :content='bookLove' :num='0' v-show='show'  v-if='!Loveshow' @acceptfromchild='showId'></MyBookList>
                        <MyBookDetail v-show='!show' :site='bookDetail' :star='bookDetail.grade/2'></MyBookDetail>
                    </Col>
                    <Col :xl="{span:7,offset:1}" :xs="{span:24}" style="margin-top:.33rem">
                        <span>书籍排行榜</span>
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
      bookLove: [

      ],
      more: 4,
      moreback: '更多',
      show: true,
      Loveshow: true,
      bookDetail: [

      ],
      womensort:[

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
    OutputWomenLove () {
      const msg = this.$Message.loading({
        content: 'Loading...',
        duration: 0
      })
      this.getWomenLoveData();
      setTimeout(msg, 3000)
      setTimeout(() => {
        this.Loveshow = !this.Loveshow
      }, 3000)
    },
    getData () {
      Axios.get('api/book/topBook').then((book) => {
        this.books = book.data
        console.log(book.data)
      })
    },
    getWomenLoveSort () {
      Axios.get('api/book/get/femaleSort').then((book) => {
        this.womensort=book.data;
        console.log(book.data)
      })
    },
     getWomenLoveData () {
      Axios.get('api/book/getBySortNum/'+this.womensort.sort+'/10').then((book) => {
        this.bookLove=book.data;
        console.log(this.bookLove)
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
    this.getData();
    this.getWomenLoveSort();
    
  }
}
</script>
<style scoped>
.book_button{
  padding: 0;
  color:#000;
  margin-right: .5rem;
}
.content{
    padding:.23rem 0.5rem 0 1rem;
    background-color: #fff;
}
.content hr{
    padding: 0;
    color: #fff
}
.title{
    font-size: 16px;
    line-height:38px;
}
</style>
