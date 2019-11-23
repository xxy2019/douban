<template>
<div class="mylist">
    <List item-layout="vertical">
        <ListItem v-for="(item,index) in content.slice(num,10)" :key="index" class="list">
            <ListItemMeta>
                <template slot="avatar">
                    <img :src="'https://images.weserv.nl/?url='+item.cover" class="list_img" @click="sendToparent(item.id)"/>
                </template>
                <template slot="title">
                    <li style="font-size:0.3rem" class="book_title">{{item.name}}</li>
                </template>
                <template slot="description">
                    <li class="book_description">{{'书籍名称:'+item.name}}</li>
                    <li class="book_description">{{"作者:"+item.author}}</li>
                </template>
        </ListItemMeta>
        </ListItem>
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
.list{
    width: 7.3rem;
    float: left;
    border: none;
    align-content: left;
}
.list_img{
    width:2.3rem;
    height: 3rem;
    margin-right:0.2rem
}
.book_title{
  width: 4rem;
}
.book_description{
  width: 8rem;
  font-size: 0.25rem
}
</style>
