<template>
    <div class="footer">
        <span class="total-elem">Всего элементов: {{this.lengthData}} </span>
    </div>
</template>

<script>
    export default {
        props: ['renderData'],
        computed: {
            lengthData() {
                return this.renderData.length
            }
        },
    }
</script>

<style scoped>
    .footer {
        width: calc(100% - 60px);
        height: 81px;
        display: flex;
        justify-content: flex-end;
        align-items: center;
        margin-right: 30px;
        margin: 0 auto;
    }

    .total-elem {
        font-size: 16px;
    }
</style>