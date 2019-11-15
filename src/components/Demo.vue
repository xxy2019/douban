<template>
    <Button @click="confirm">导出榜单</Button>
</template>
<script>
    export default {
        methods: {
            confirm () {
                this.$Modal.confirm({
                    content: '<p>您需要导出榜单吗？</p><p>请您仔细考虑</p>',
                    onOk: () => {
                        this.$Message.info('确定');
                    },
                    onCancel: () => {
                        this.$Message.info('取消');
                    }
                });
            }
        }
    }
</script>
