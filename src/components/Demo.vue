<template>      
    <li @click='handleItemClick'>{{content}}</li>
</template>
<script>
export default {
    name:'Demo',
    props:['content','index'],
    methods:{
        handleItemClick:function(){
            this.$emit('delete',this.index)
        }
    }
}
</script>