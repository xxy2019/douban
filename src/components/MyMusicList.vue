<template>
<div class="mylist">
    <List item-layout="vertical">
      <Row>
      <ListItem v-for="item in content" :key="item.id" class="list">
        <Col :xl='12' :xs="24">
        <ListItemMeta>
          <template slot="avatar">
             <img :src="'https://images.weserv.nl/?url='+item.coverUrl" class="list_img" @click="sendIdToparent(item.id)"/>
          </template>
          <template slot="title">
            <li>{{item.name}}</li>
          </template>
          <template slot="description">
            <li>{{'表演者:'+item.singer}}</li>
            <li>{{"流派:"+item.style}}</li>
            <li>{{"发行时间:"+item.issueDate.substring(0,10)}}</li>
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
  name: 'MyMusicList',
  data () {
    return {
    }
  },
  props: ['content'],
  methods: {
    handleScroll () {
      let scrolltop = document.documentElement.scrollTop || document.body.scrollTop
      scrolltop > 30 ? (this.gotop = true) : (this.gotop = false)
    },
    sendIdToparent: function (value) {
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
  }
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
    width:116px;
    height: 134px;
    margin-right:16px;
    margin-bottom: 10px;
}
</style>

