<template>
  <div class="text">
    <ul>
      <li v-for="site in sites" :key="site.id" class="enum_list">
        <img :src="site.pic" alt=""  id="m_pic">
        <div class="detail">
          <li class="d_title">{{'电影名称：'+site.d_name}}</li>
          <p id="daoyian">
            {{'导演：'+site.daoyian}}
          </p>
          <p id="bianj">
            {{'编剧: '+site.bianju}}
          </p>
          <p id="zhuyan">
          {{'主演: '+site.zhuyan}}
          </p>
          <p id="leixin">
          {{'类型: '+site.leixin}}
          </p>
          <p id="guoj">
          {{'制片国家/地区:'+site.guojia}}
          </p>
        </div>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  name: 'MyText',
  data () {
    return {
      sites: [
        {
          d_name: '少年的你',
          pic: require('../assets/pic1.jpg'),
          daoyian: '曾国祥',
          bianju: '林咏琛 / 李媛 / 许伊萌',
          zhuyan: '周冬雨 / 易烊千玺 / 尹昉 / 黄觉 / 吴越 / 更多...',
          leixin: '剧情 / 爱情',
          guojia: ' 中国大陆'

        },
        {
          d_name: '少年的你',
          pic: require('../assets/pic1.jpg'),
          daoyian: '曾国祥',
          bianju: '林咏琛 / 李媛 / 许伊萌',
          zhuyan: '周冬雨 / 易烊千玺 / 尹昉 / 黄觉 / 吴越 / 更多...',
          leixin: '剧情 / 爱情',
          guojia: ' 中国大陆'

        },
        {
          d_name: '少年的你',
          pic: require('../assets/pic1.jpg'),
          daoyian: '曾国祥',
          bianju: '林咏琛 / 李媛 / 许伊萌',
          zhuyan: '周冬雨 / 易烊千玺 / 尹昉 / 黄觉 / 吴越 / 更多...',
          leixin: '剧情 / 爱情',
          guojia: ' 中国大陆'

        }
      ]
    }
  }
}
</script>
<style scoped>
.text{
  width:21.8rem;
  height:34.1875rem;
  background-color: #f7f7f7;
  margin-top: 1.875rem;
  margin-left: 1.725rem;
  float:left;
}
ul,li{
  list-style: none;
}
.enum_list{
  width:18.25rem;
  height:8.3125rem;
  margin-top: .8125rem;
}
#m_pic{
  width:5.5rem;
  height:8.375rem;
  float:left;
}
.detail{
  width:12rem;
  height:8.5rem;
  float:right;
}
.d_title{
  margin-left:.3125rem;
  font-size:.75rem;
  height:.9375rem;
  width:11.375rem;
  font-weight:bold;
}
.detail p{
  margin:.3125rem ;
  font-size: .625rem;
}
</style>
