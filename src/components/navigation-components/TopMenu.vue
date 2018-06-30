<template>
    <nav class="top-menu">
        <div class="date">{{formattedDate}}</div>
    </nav>
</template>

<script>
    import moment from 'moment'

    export default {
        name: "top-menu",

        data() {
            return {
                formattedDate: moment().format('DD-MM-YYYY')

            }
        }


    }
</script>

<style scoped lang="less">
    @import (reference) '../../assets/less/mainstyles.less';

    .top-menu {
        background-color: @primaryColor;
        width: 100vw;
        height: 75px;

        .date {
            color: @white;
            font-weight: bold;
            font-size: 40px;
            padding: 8px 0 0 20px;
            border-right-width: 3px;
            width: 305px;
            height: 75px;

        }
    }


</style>