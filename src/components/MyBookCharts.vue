<template>
    <div>
        <List>
            <ListItem class='listitem' v-for="(item,index) in content" :key="item.index">
                <Col :xs="24" :xl="24">
                   <Icon type="ios-ribbon"  :class="JudgeClass[index]" v-if='index<3'/>
                   <span v-if='index>2'>{{index+1+"、"}}</span>{{item.name+" by"+item.author}}
                </Col>
            </ListItem>
        </List>
    </div>
</template>
<script>
    export default {
        name:'MyBookCharts',
        props:['content'],
         data () {
    return {
      JudgeClass: ['gold', 'silver', 'copper']
    }
  }
    }
</script>
<style scoped>
.listitem{
    border: none;
}
.gold{
   font-size:.325rem;
   color:gold;
}
.silver{
   font-size:.325rem;
   color:silver;
}
.copper{
   font-size:.325rem;
   color:#b87333 ;
}
</style>
