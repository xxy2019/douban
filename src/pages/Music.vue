<template>
<div class="layout">
    <Layout>
        <Header></Header>
        <Layout>
            <Content class="content">
                <Row>
                    <Col span="16">
                    <Row>
                      <Col span="6" ><span style="line-height:3rem">音乐热评榜</span></Col>
                      <Col span="4" offset="14"><Button  size='large' icon="ios-arrow-back" type="text" v-show="!show" @click="change" id="back">返回</Button></Col>
                    </Row>
                        <hr><hr>
                        <MyMusicList :content='musics' @accepttochild="showId" v-show='show'></MyMusicList>
                        <MyMusicDetail v-show='!show' :site='musicDetail' :star='musicDetail.reviewScore/2'></MyMusicDetail>
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
    getMusicExcel () {
      Axios.get('/api/music/get/topNToExcel').then((excel) => {
        this.excel = excel.data
        console.log(excel)
      })
    },
    getMusicTopData () {
      return Axios({
        method: 'get',
        baseURL: 'api',
        url: '/music/get/top',
        timeout: 1000
      })
    },
    getData () {
      Axios.all([this.getMusicTopData()])
        .then(Axios.spread((music) => {
          this.musics = music.data
          console.log(music.data)
        })).catch(function (error) {
          console.log(error)
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
