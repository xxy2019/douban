<template>
<div class="mylist">
    <List item-layout="vertical">
        <ListItem v-for="(item,index) in content.slice(num,30)" :key="index" class="list">
            <ListItemMeta>
                <template slot="avatar">
                    <img :src="'https://images.weserv.nl/?url='+item.coverUrl" class="list_img" @click="sendIdToparent(item.id)"/>
                </template>
                <template slot="title">
                    <li style="font-size:0.3rem" class="movie_title">{{item.name}}</li>
                </template>
                <template slot="description">
                    <li class="movie_description">{{'导演:'+item.director}}</li>
                    <li class="movie_description">{{"编剧:"+item.screenwriter.substring(0,10)}}<span style="color:#555"> 更多</span></li>
                    <li class="movie_description">{{"主演:"+item.starring.substring(0,16)}}<span style="color:#555"> 更多</span></li>
                    <li class="movie_description">{{"类型："+item.type}}</li>
                    <li class="movie_description">{{"上映时间"+item.date}}</li>
                </template>
        </ListItemMeta>
        </ListItem>
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
    width: 7.2rem;
    float: left;
    border: none;
    align-content: left;
}
.list_img{
    width:2.3rem;
    height: 3rem;
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
