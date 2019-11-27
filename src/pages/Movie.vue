<template>
<div class="layout">
    <Layout>
        <router-link :to="{path:'/'}"><Header></Header></router-link>
        <Layout>
            <Content class="content">
                <Row>
                    <Col :xl="16" :xs="24">
                        <Row>
                            <Col :xl="{span:5,offset:0}" :xs="{span:11,offset:0}"><span class='title'>电影热评榜</span></Col>
                            <Col :xl="{span:2,offset:17}" :xs="{span:3,offset:8}">
                                <Button size='large' type="text" @click="OutputMore" v-show="show">更多</Button>
                                <Button size='large' type="text" @click="back" v-show="!show">返回</Button>
                            </Col>
                        </Row>
                        <hr/>
                        <MyMovieList :content='movies' :num='more' @accepttochild="showId" v-show='show'></MyMovieList>
                        <MyMovieDetail v-show='!show' :site='movieDetail' :star='movieDetail.score/2'></MyMovieDetail>
                    </Col>
                    <Col :xl="{span:7,offset:1}" :xs="{span:24}" style="margin-top:.33rem">
                        <span>电影排行榜</span>
                        <hr/>
                        <MyMovieCharts :content='movies'></MyMovieCharts>
                    </Col>
                </Row>  
            </Content>
        </Layout>
    </Layout>
</div>
</template>
<script>
import MyHeader from '../components/MyHeader'
import MyMovieList from '../components/MyMovieList'
import MyMovieCharts from '../components/MyMovieCharts'
import MyMovieDetail from '../components/MyMovieDetail'
import Axios from 'axios'
export default {
  name: 'Movie',
  components: {
    MyMovieList: MyMovieList,
    Header: MyHeader,
    MyMovieCharts: MyMovieCharts,
    MyMovieDetail
  },
  data () {
    return {
      movies: [

      ],
      more: 8,
      moreback: '更多',
      show: true,
      movieDetail: [

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
      Axios.get('api/movie/topMovies/30').then((movie) => {
        this.movies = movie.data
        console.log(movie.data)
      })
    },
    showId (value) {
      console.log(value)
      Axios.get('api/movie/get/' + value).then((movieDetail) => {
        this.movieDetail = movieDetail.data
        this.show = false
        this.moreback = '返回'
        console.log(this.movieDetail)
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
    padding:.25rem 0.5rem 0 1rem;
    background-color: #fff;
}
.content hr{
    padding: 0;
}
.title{
    font-size: 16px;
    line-height:38px;
}
</style>
