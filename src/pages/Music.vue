<template>
<div class="layout">
    <Layout>
        <Header>Header</Header>
        <Layout>
            <Content class="content">
                <Row>
                    <Col span="16">
                        <Row>
                            <Col span="2"><span>音乐热评表</span></Col>
                            <Col span="4" offset="18"><Button :size="buttonSize" icon="ios-download-outline" type="primary">导出榜单</Button></Col>
                        </Row>
                        <hr><hr>
                        <MyList></MyList>
                    </Col>
                    <Col span="8">
                    </Col>
                </Row>   
            </Content>
        </Layout>
        <Footer>Footer</Footer>
    </Layout>
</div>
</template>
<script>
import MyHeader from '../components/MyHeader'
import MyList from '../components/MyList'
export default {
    name:'Music',
    components:{
        MyList:MyList,
        Header:MyHeader,
    },
}
</script>
<style scoped>
.content{
    margin:2em 2em 0 2em;
}
.content hr{
    padding: 0;
    margin:0;
    border: solid 0.01em #dcdee2;
}
</style>