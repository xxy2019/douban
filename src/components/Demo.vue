<template>
    <div>
      <Row>
        <List>
            <ListItem class='listitem' v-for="(item,index) in musics" :key="item.index">
              <Col :xs="24" :sm="12" :md="12" :lg="12" style="font-size:0.23rem">
                {{index+1+'、'+item.name+" by"+item.singer}}
              </Col>
            </ListItem>
        </List>
      </Row>
    </div>
</template>
<script>
import Axios from 'axios'
export default {
  name: 'MyMusicCharts',
  props: ['content'],
  data () {
    return {
      musics:[

      ]
    }
  },
  methods: {
    getData(){
        Axios.get('api/music/get/top').then((music)=>{
             this.musics=music.data;
             console.log(music.data)
        })
    },
  },
  created () {
    this.getData()
  }
}
</script>
<style scoped>
.listitem{
    border: none;
}
</style>
