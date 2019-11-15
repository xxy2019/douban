<template>
<div class="layout">
    <Layout>
        <Header></Header>
        <Layout>
            <Content class="content">
                <Row>
                    <Col span="16">
                        <Row>
                            <Col span="3"><span>音乐热评榜</span></Col>
                            <Col span="4" offset="17"><Button :loading=isloading icon="ios-download-outline" type="text" @click="OutputExcel">导出榜单</Button></Col>
                        </Row>
                        <hr><hr>
                        <MyList :content='musics'></MyList>
                    </Col>
                    <Col span="7" offset='1' style="margin-top:1.2rem">
                        <span class='title'>音乐排行榜</span>
                        <hr><hr>
                        <MyCharts :content='tops'></MyCharts>
                    </Col>
                </Row>  
            </Content>
        </Layout>
    </Layout>
</div>
</template>
<script>
import MyHeader from '../components/MyHeader'
import MyList from '../components/MyList'
import MyCharts from '../components/MyCharts'
import Axios from 'axios'
export default {
    name:'Music',
    components:{
        MyList:MyList,
        Header:MyHeader,
        MyCharts:MyCharts
    },
    data(){
        return{
            tops:[
                
            ],
            musics:[

            ],
            isloading:false,
            excel:[

            ]
        }
    },
    methods:{
        OutputExcel(){
            this.isloading=true;
            this.$Modal.confirm({
                content: '<p>您需要导出榜单吗？</p><p>请您仔细考虑！</p>',
                onOk: () => {
                    this.$Message.info('确定');
                    this.getMusicExcel();
                },
                onCancel: () => {
                    this.$Message.info('取消');
                }
            });
            this.isloading=false;
        },
        getMusicExcel(){
            Axios.get('/api/music/get/topNToExcel').then((excel)=>{
                this.excel=excel.data;
                console.log(excel);
            })
        },
        getMusicData(){
        return Axios({
          method:'get',
          baseURL:'api',
          url:'/music/get',
        })
        },
        getMusicTopData(){
        return Axios({
          method:'get',
          baseURL:'api',
          url:'/music/get/topN',
          timeout:1000
        })
        },
        getData(){
        Axios.all([this.getMusicData(),this.getMusicTopData()])
        .then(Axios.spread((music,musictop)=>{
          this.tops=musictop.data;
          this.musics=music.data;           
          console.log(music.data);
        })).catch(function(error){
            console.log(error)
        });
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