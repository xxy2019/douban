<template>
<div class="layout">
    <Layout>
        <Header></Header>
        <Layout>
            <Content class="content">
                <Row>
                    <Col span="16">
                        <span style="line-height:3rem">音乐热评榜</span>
                        <hr><hr>
                        <MyMusicList :content='musics'></MyMusicList>
                    </Col>
                    <Col span="7" offset='1' style="margin-top:1.2rem">
                        <Row>
                            <Col span="6" ><span class='title' style="line-height:2rem">音乐排行榜</span></Col>
                            <Col span="6" offset="12"><Button  size='small' icon="ios-download-outline" type="text" @click="OutputExcel">导出榜单</Button></Col>
                        </Row>
                        <hr><hr>
                        <MyMusicCharts :content='musics'></MyMusicCharts>
                    </Col>
                </Row>  
            </Content>
        </Layout>
    </Layout>
</div>
</template>
<script>
import MyHeader from '../components/MyHeader'
import MyMusicList from '../components/MyMusicList'
import MyMusicCharts from '../components/MyMusicCharts'
import Axios from 'axios'
export default {
    name:'Music',
    components:{
        MyMusicList:MyMusicList,
        Header:MyHeader,
        MyMusicCharts:MyMusicCharts
    },
    data(){
        return{
            musics:[

            ],
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
            Axios({
                    url:'/api/music/get/topNToExcel',
                    method: 'get',
                    responseType: 'blob'
                }).then((response) => {
                    const blob = new Blob(
                        [response.data], { type: 'application/vnd.openxmlformats-officedocument.spreadsheetml.sheet;charset=utf-8' })
                    const aEle = document.createElement('a');     // 创建a标签
                    const href = window.URL.createObjectURL(blob);       // 创建下载的链接
                    aEle.href = href;
                    aEle.download = "音乐榜单.xls";  // 下载后文件名
                    document.body.appendChild(aEle);
                    aEle.click();     // 点击下载
                    document.body.removeChild(aEle); // 下载完成移除元素
                    window.URL.revokeObjectURL(href) // 释放掉blob对象
                }).catch((error) => {
                    console.log(error);
                });
        },
        getData(){
            Axios.get('api/music/get/top').then((music)=>{
                 this.musics=music.data;
                 console.log(music.data)
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