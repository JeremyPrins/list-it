<template>
<nav class="top-menu">
    <div class="date">19-06-2018</div>
</nav>
</template>

<script>
    export default {
        name: "top-menu"
    }
</script>

<style scoped lang="less">
    @import (reference) '../../assets/less/mainstyles.less';

    .top-menu{
        background-color: @yellow;
        width: 100vw;
        height: 75px;

        .date {
            color: @white;
            font-weight: bold;
            font-size: 40px;
            padding: 5px 0 0 50px;
            border-color: @white;
            border-style: solid;
            border-width: 0 3px 3px 0;

            width: 305px;
            height: 75px;

        }
    }


</style>