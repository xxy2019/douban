<template>
    <div>
      <Row>
        <List>
            <ListItem class='listitem' v-for="(item,index) in content" :key="item.index">
              <Col :xs="24" :sm="12" :md="12" :lg="12" style="font-size:0.23rem">
                <Icon type="ios-ribbon"  :class="JudgeClass[index]" v-if='index<3'/>
<span v-if='index>2'>{{index+1+"、"}}</span>{{item.name+" by"+item.singer}}
              </Col>
            </ListItem>
        </List>
      </Row>
    </div>
</template>
<script>
export default {
  name: 'MyMusicCharts',
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
