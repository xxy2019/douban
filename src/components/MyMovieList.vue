<template>
<div class="mylist">
    <List item-layout="vertical">
      <Row> 
        <ListItem v-for="(item,index) in content.slice(num,30)" :key="index" class="list">
            <Col :xl='12' :xs="24">
            <ListItemMeta>
                <template slot="avatar">
                    <img :src="'https://images.weserv.nl/?url='+item.coverUrl" class="list_img" @click="sendIdToparent(item.id)"/>
                </template>
                <template slot="title">
                    <li>{{item.name}}</li>
                </template>
                <template slot="description">
                    <li>{{'导演:'+item.director}}</li>
                    <li>{{"编剧:"+item.screenwriter.substring(0,10)}}<span style="color:#555"> 更多</span></li>
                    <li>{{"主演:"+item.starring.substring(0,16)}}<span style="color:#555"> 更多</span></li>
                    <li>{{"类型："+item.type}}</li>
                    <li>{{"上映时间"+item.date}}</li>
                </template>
          </ListItemMeta>
          </Col>  
        </ListItem>
        </Row>
    </List>
</div>
</template>
<script>
export default {
  name: 'MyMovieList',
  data () {
    return {
    }
  },
  methods: {
    handleScroll () {
      let scrolltop = document.documentElement.scrollTop || document.body.scrollTop
      scrolltop > 30 ? (this.gotop = true) : (this.gotop = false)
    },
    sendIdToparent (value) {
      console.log(value)
      this.$emit('accepttochild', value)
      let top = document.documentElement.scrollTop || document.body.scrollTop
      const timeTop = setInterval(() => {
        document.body.scrollTop = document.documentElement.scrollTop = top -= 50
        if (top <= 0) {
          clearInterval(timeTop)
        }
      }, 10)
    }
  },
  props: ['content', 'num']
}
</script>
<style scoped>
.list{
    border: none;
    align-content: left;
    padding: 0px;
    margin-top: 20px; 
}
.list_img{
    width:132px;
    height: 172px;
    margin-right:0.2rem;
    margin-bottom: 10px;
}
</style>
