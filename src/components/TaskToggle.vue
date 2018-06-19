<template>
    <div class="task-toggle-container">
        {{title}} ({{todosCount}})
    </div>
</template>

<script>
    export default {
        props: ['todosCount', 'title'],
    name: "task-toggle",

    }
</script>

<style scoped lang="less">
    @import (reference) '../assets/less/mainstyles.less';

    .task-toggle-container {
        font-size: 40px;
        font-weight: bolder;
        color: @yellow;
        width: 100%;
        display: block;
        padding: 40px 0 0 20px;
        border-bottom: @yellow 3px solid;

    }

</style>