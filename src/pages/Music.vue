<template>
<div class="layout">
    <Layout>
        <router-link :to="{path:'/'}"><Header></Header></router-link>
        <Layout>
            <Content class="content">
                <Row>
                    <Col :xl="16" :xs="13">
                    <Row>
                      <Col :xl="{span:5,offset:0}" :xs="{span:11,offset:0}"><span>音乐热评榜</span></Col>
                      <Col :xl="{span:3,offset:16}" :xs="{span:7,offset:6}"><Button  size='small' icon="ios-arrow-back" type="text" v-show="!show" @click="change">返回</Button></Col>
                    </Row>
                        <hr/>
                        <MyMusicList :content='musics' @accepttochild="showId" v-show='show'></MyMusicList>
                        <MyMusicDetail v-show='!show' :site='musicDetail' :star='musicDetail.reviewScore/2'></MyMusicDetail>
                    </Col>
                    <Col :xl="{span:7,offset:1}" :xs="{span:10,offset:1}">
                        <Row>
                            <Col :xl="6" :xs="12"><span class="title">音乐排行榜</span></Col>
                            <Col :xl="{span:6,offset:12}" :xs="{span:11,offset:1}"><Button class="title" size='small' icon="ios-download-outline" type="text" @click="OutputExcel">导出榜单</Button></Col>
                        </Row>
                        <hr/>
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
import MyMusicDetail from '../components/MyMusicDetail'
import Axios from 'axios'
export default {
  name: 'Music',
  components: {
    MyMusicList: MyMusicList,
    Header: MyHeader,
    MyMusicCharts: MyMusicCharts,
    MyMusicDetail
  },
  data () {
    return {
      musics: [

      ],
      isloading: false,
      excel: [

      ],
      musicDetail: [

      ],
      show: true
    }
  },
  methods: {
    change () {
      this.show = true
    },
    OutputExcel () {
      this.isloading = true
      this.$Modal.confirm({
        content: '<p>您需要导出榜单吗？</p><p>请您仔细考虑！</p>',
        onOk: () => {
          this.$Message.info('确定')
          this.getMusicExcel()
        },
        onCancel: () => {
          this.$Message.info('取消')
        }
      })
      this.isloading = false
    },
    getData(){
        Axios.get('api/music/get/top').then((music)=>{
             this.musics=music.data;
             console.log(music.data)
        })
    },
    change () {
      this.show = true
    },
    getMusicExcel () {
      Axios({
        url:'api/music/get/topNToExcel',
        method:'get',
        responseType:'blob'
      }).then((response)=>{
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
    getMusicTopData () {
      return Axios({
        method: 'get',
        baseURL: 'api',
        url: '/music/get/top',
        timeout: 1000
      })
    },
    showId (value) {
      console.log(value)
      Axios.get('api/music/get/' + value).then((musicDetail) => {
        this.musicDetail = musicDetail.data
        this.show = false
        console.log(this.musicDetail)
      })
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
    color: #fff
}
.title{
  font-size: .23rem;
  line-height:.2rem
}
</style>
