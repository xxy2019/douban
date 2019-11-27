<template>
<div class="mylist">
    <List item-layout="vertical">
      <Row>
        <ListItem v-for="(item,index) in content.slice(num,10)" :key="index" class="listitem">
            <Col :xl='12' :xs="24">
            <ListItemMeta>
                <template slot="avatar">
                    <img :src="'https://images.weserv.nl/?url='+item.cover" class="list_img" @click="sendToparent(item.id)"/>
                </template>
                <template slot="title" >
                    <li style="margin-top:40px">{{item.name}}</li>
                </template>
                <template slot="description">
                    <li>{{'书籍名称:'+item.name}}</li>
                    <li>{{"作者:"+item.author}}</li>
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
  name: 'MyBookList',
  data () {
    return {
    }
  },
  methods: {
    handleScroll () {
      let scrolltop = document.documentElement.scrollTop || document.body.scrollTop
      scrolltop > 30 ? (this.gotop = true) : (this.gotop = false)
    },
    sendToparent: function (value) {
      this.$emit('acceptfromchild', value)
      console.log(value)
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
.listitem{
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
