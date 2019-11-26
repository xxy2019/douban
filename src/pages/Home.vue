<template>
<div class="layout">
    <Layout>
        <Header :to='{path:"/"}'></Header>
        <Layout>
            <Content class="content">
                <Row>
                    <Col :xl="16" :xs="24">
                        <Row>
                            <Col :xl="{span:5,offset:0}" :xs="{span:11,offset:0}"><span class="title">亚洲热评视频</span></Col>
                            <Col :xl="{span:2,offset:17}" :xs="{span:3,offset:8}">
                                <Button type="text" :to='{path:"/Movie"}'>更多</Button>
                            </Col>
                        </Row>
                        <hr/>
                        <Row>
                        <MyMovieList :content='movies' :num='more'></MyMovieList>
                        </Row>
                    </Col>
                    <Col :xl="{span:7,offset:1}" :xs="{span:24}">
                        <Row style="margin-top:.24rem">
                            <Col :xl="6" :xs="10"><span>音乐排行榜</span></Col>
                            <Col :xl="{span:6,offset:12}" :xs="{span:5,offset:9}"><Button size='small' type="text" :to='{path:"/Music"}'>更多</Button></Col>
                        </Row>
                        <hr/>
                        <Row>
                        <MyMusicCharts :content='musics'></MyMusicCharts>
                        </Row>
                    </Col>
                </Row>
                 <Row style="margin-top:1rem">
                    <Col :xl="{span:5,offset:0}" :xs="{span:10,offset:0}"><span class="title">亚洲热评书籍</span></Col>
                     <Col :xl="{span:9,offset:10}" :xs="{span:5,offset:9}">
                      <Button type="text" :to='{path:"/Book"}'>更多</Button>
                    </Col>
                 </Row>
                 <Row>
                    <Col :xl='16' :xs='24'><hr/><MyBookList :content='books'></MyBookList></Col>
                 </Row>  
            </Content>
        </Layout>
    </Layout>
</div>
</template>
<script>
import MyHeader from '../components/MyHeader'
import MyMovieList from '../components/MyMovieList'
import MyMusicCharts from '../components/MyMusicCharts'
import MyBookList from '../components/MyBookList'
import Axios from 'axios'
export default {
    name:'Home',
    components:{
        MyMovieList:MyMovieList,
        Header:MyHeader,
        MyMusicCharts:MyMusicCharts,
        MyBookList:MyBookList
    },
    data(){
        return{
            movies:[

            ],
            musics:[

            ],
            books:[

            ],
            more:0,
        }
    },
    methods:{
        OutputMore(){
            const msg = this.$Message.loading({
                    content: 'Loading...',
                    duration: 0,
                });
            setTimeout(msg, 3000);a
            setTimeout(()=>{
                this.more=0
            },3000)
        },
        getMovieData(){
          return Axios({
            method:'get',
            baseURL:'api',
            url:'/movie/topMovies/10'
          })
        },
        getMusicData(){
          return Axios({
            method:'get',
            baseURL:'api',
            url:'/music/get/top10'
          })
        },
        getBookData(){
          return Axios({
            method:'get',
            baseURL:'api',
            url:'/book/topBook'
          })
        },
        getData(){
            Axios.all([this.getMovieData(),this.getMusicData(),this.getBookData()])
            .then(Axios.spread((movie,music,book)=>{
              this.movies=movie.data;
              this.musics=music.data;
              this.books=book.data
            }))
        },
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
    margin:0;
}
.title{
    font-size: 16px;
    line-height:38px;
}
</style>
