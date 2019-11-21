<template>
<div class="mylist">
    <List item-layout="vertical">
        <ListItem v-for="(item,index) in content.slice(0,40)" :key="index" class="list">
            <ListItemMeta>
                <template slot="avatar">
                    <img :src="'https://images.weserv.nl/?url='+item.coverUrl" class="list_img" @click="sendIdToparent(item.id)"/>
                </template>
                <template slot="title">
                    {{item.name}}
                </template>
                <template slot="description">
                    <li>{{'表演者:'+item.singer}}</li>
                    <li>{{"流派:"+item.style}}</li>
                    <li>{{"发行时间:"+item.issueDate}}</li>
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
    width: 26rem;
    float: left;
    border: none;
    align-content: left;
}
.list_img{
    width:7rem;
    height: 8rem;
    margin-right:2rem
}
</style>
