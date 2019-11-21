<template>
<div class="mylist">
    <List item-layout="vertical">
        <ListItem v-for="(item,index) in content.slice(num,30)" :key="index" class="list">
            <ListItemMeta>
                <template slot="avatar">
                    <img :src="'https://images.weserv.nl/?url='+item.coverUrl" class="list_img" @click="sendIdToparent(item.id)"/>
                </template>
                <template slot="title" class="title">
                    {{item.name}}
                </template>
                <template slot="description">
                    <li>{{'导演:'+item.director}}</li>
                    <li>{{"编剧:"+item.screenwriter.substring(0,10)}}<span style="color:#555"> 更多</span></li>
                    <li>{{"主演:"+item.starring.substring(0,16)}}<span style="color:#555"> 更多</span></li>
                    <li>{{"类型："+item.type}}</li>
                    <li>{{"上映时间"+item.date}}</li>
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
    sendIdToparent (value) {
      console.log(value)
      this.$emit('accepttochild', value)
    }
  },
  props: ['content', 'num']
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
    width:8rem;
    height: 11rem;
    margin-right:1rem
}
</style>
