<template>
<div class="layout">
    <Layout>
        <Header></Header>
        <Layout>
            <Content class="content">
                <Row>
                    <Col span="16">
                        <Row>
                            <Col span="3"><span>书籍热评榜</span></Col>
                            <Col span="2" offset="19">
                                <Button size='small' type="text" @click="OutputMore">更多</Button>
                            </Col>
                        </Row>
                        <hr><hr>
                        <MyBookList :content='books' :num='more'></MyBookList>
                    </Col>
                    <Col span="7" offset='1' style="margin-top:1.2rem">
                        <span class='title'>书籍排行榜</span>
                        <hr><hr>
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
import Axios from 'axios'
export default {
    name:'Book',
    components:{
        MyBookList:MyBookList,
        Header:MyHeader,
        MyBookCharts:MyBookCharts
    },
    data(){
        return{
            books:[

            ],
            more:4,
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
            Axios.get('api/book/topBook').then((book)=>{
                 this.books=book.data;
                 console.log(book.data)
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
