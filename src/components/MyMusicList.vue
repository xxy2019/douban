<template>
<div class="mylist">
    <List item-layout="vertical">
      <ListItem v-for="item in content" :key="item.id" class="list">
        <ListItemMeta>
          <template slot="avatar">
             <img :src="'https://images.weserv.nl/?url='+item.coverUrl" class="list_img" @click="sendIdToparent(item.id)"/>
          </template>
          <template slot="title">
            <li style="font-size:0.3rem" class="movie_title">{{item.name}}</li>
          </template>
          <template slot="description">
            <li class="movie_description">{{'表演者:'+item.singer}}</li>
            <li class="movie_description">{{"流派:"+item.style}}</li>
            <li class="movie_description">{{"发行时间:"+item.issueDate.substring(0,10)}}</li>
          </template>
        </ListItemMeta>
      </ListItem>    
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
    width: 7.2rem;
    float: left;
    border: none;
    align-content: left;
}
.list_img{
    width:2rem;
    height: 2.3rem;
    margin-right:0.2rem
}
.movie_title{
  width: 4rem;
}
.movie_description{
  width: 8rem;
  font-size: 0.25rem
}
</style>

