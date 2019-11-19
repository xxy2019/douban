<template>
<div class="layout">
    <Layout>
        <Header></Header>
        <Layout>
            <Content class="content">
                <Row>
                    <Col span="16">
                        <Row>
                            <Col span="3"><span>电影热评榜</span></Col>
                            <Col span="2" offset="19">
                                <Button size='small' type="text" @click="OutputMore">更多</Button>
                            </Col>
                        </Row>
                        <hr><hr>
                        <MyMovieList :content='movies' :num='more'></MyMovieList>
                    </Col>
                    <Col span="7" offset='1' style="margin-top:1.2rem">
                        <span class='title'>电影排行榜</span>
                        <hr><hr>
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
import Axios from 'axios'
export default {
    name:'Movie',
    components:{
        MyMovieList:MyMovieList,
        Header:MyHeader,
        MyMovieCharts:MyMovieCharts
    },
    data(){
        return{
            movies:[

            ],
            more:8,
        }
    },
    methods:{
        OutputMore(){
            const msg = this.$Message.loading({
                    content: 'Loading...',
                    duration: 0,
                });
            setTimeout(msg, 3000);
            setTimeout(()=>{
                this.more=0
            },3000)
        },
        getData(){
            Axios.get('api/movie/topMovies').then((movie)=>{
                 this.movies=movie.data;
                 console.log(movie.data)
            })
        }
    },
    created(){
      this.getData();
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
    border: solid 0.01em #dcdee2;
}
.title{
    position: relative;
    top: -.3rem;
}
</style>
