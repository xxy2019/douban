<template>
<div class="layout">
    <Layout>
        <Header :to='{path:"/"}'></Header>
        <Layout>
            <Content class="content">
                <Row>
                    <Col :xs="12" :xl="16">
                        <Row>
                            <Col :xs="2" :xl="3"><span style="line-height:2rem">亚洲热评视频</span></Col>
                            <Col :xs="{span:2,offset:19}" :xl="{span:2,offset:19}">
                                <Button size='small' type="text" :to='{path:"/Movie"}'>更多</Button>
                            </Col>
                        </Row>
                        <hr/>
                        <Row>
                        <MyMovieList :content='movies' :num='more'></MyMovieList>
                        </Row>
                    </Col>
                    <Col span="7" offset='1' style="margin-top:1.2rem">
                        <Row>
                            <Col span="6" ><span class='title' style="line-height:2rem">音乐排行榜</span></Col>
                            <Col span="6" offset="12"><Button size='small' type="text" :to='{path:"/Music"}'>更多</Button></Col>
                        </Row>
                        <hr/>
                        <Row>
                        <MyMusicCharts :content='musics'></MyMusicCharts>
                        </Row>
                    </Col>
                </Row>
                 <Row style="margin-top:2rem">
                    <Col span="3"><span>亚洲热评书籍</span></Col>
                    <Col span="2" offset="12">
                      <Button size='small' type="text" :to='{path:"/Book"}'>更多</Button>
                    </Col>
                 </Row>
                 <Row>
                    <Col span="16"><hr/><MyBookList :content='books'></MyBookList></Col>
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
    padding:2em 3rem 0 3rem;
    background-color: #fff;
}
.content hr{
    padding: 0;
    margin:0;
}
.title{
    position: relative;
    top: -.3rem;
}
</style>
