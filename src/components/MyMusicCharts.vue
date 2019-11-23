<template>
    <div>
      <Row>
        <List>
            <ListItem class='listitem' v-for="(item,index) in content" :key="item.index">
              <Col :xs="24" :sm="12" :md="12" :lg="12" style="font-size:0.23rem">
                {{index+1+'、'+item.name+" by"+item.singer}}
              </Col>
            </ListItem>
        </List>
      </Row>
    </div>
</template>
<script>
export default {
  name: 'MyMusicCharts',
  props: ['content']
}
</script>
<style scoped>
.listitem{
    border: none;
}
</style>
