<template>
    <div>
        <List>
            <ListItem class='listitem' v-for="(item,index) in content" :key="item.index">
                <Col :xs="24" :xl="24">
                   <Icon type="ios-ribbon"  :class="JudgeClass[index]" v-if='index<3'/>
                   <span v-if='index>2'>{{index+1+"、"}}</span>{{item.name+" by"+item.director}}
                </Col>
            </ListItem>
        </List>
    </div>
</template>
<script>
export default {
  name: 'MyMovieCharts',
  props: ['content'],
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
   color:gold;
}
.silver{
   color:silver;
}
.copper{
   color:#b87333 ;
}
</style>
