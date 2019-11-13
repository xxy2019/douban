<template>
<div class="mylist">
    <List item-layout="vertical">
        <ListItem v-for="item in movies" :key="item.id" class="list">
            <ListItemMeta :avatar="item.img_url" :title="item.name" :description="'表演者：'+item.singer"/>
        </ListItem>
    </List>
</div>
</template>
<script>
    export default {
        name: 'MyList',
        data(){
            return{
                movies:[
                    {
                        id:0,
                        img_url:require('@/assets/logo.png'),
                        name:'这一天',
                        singer:'李汶翰',
                        style:'原声',
                        date:'2019-09-06'
                    },
                    {
                        id:1,
                        img_url:require('@/assets/logo.png'),
                        name:'这一天',
                        singer:'李汶翰',
                        style:'原声',
                        date:'2019-09-06'
                    },
                    {
                        id:2,
                        img_url:require('@/assets/logo.png'),
                        name:'这一天',
                        singer:'李汶翰',
                        style:'原声',
                        date:'2019-09-06'
                    },
                ]
            }
        },
    }
</script>
<style scoped>
.mylist{
    margin-left: 2em;
}
.list{
    width: 30em;
    float: left;
}
</style>
