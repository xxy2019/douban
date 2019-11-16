<template>
<div class="mylist">
    <List item-layout="vertical">
        <ListItem v-for="item in content" :key="item.id" class="list">
            <ListItemMeta>
                <template slot="avatar">
                    <img :src="'https://images.weserv.nl/?url='+item.coverUrl" class="list_img"/>
                </template>
                <template slot="title">
                    {{item.name}}
                </template>
                <template slot="description">
                    <li>{{'表演者:'+item.singer}}</li>
                    <li>{{"流派:"+item.style}}</li>
                    <li>{{"发行时间:"+item.issueDate.substring(0,10)}}</li>
                </template>
        </ListItemMeta>
        </ListItem>
    </List>
</div>
</template>
<script>
    export default {
        name: 'MyList',
        data(){
            return{
            }
        },
        props:['content']
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
