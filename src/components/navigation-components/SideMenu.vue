<template>

    <aside class="navbar-body col-12 col-md-2">
        <nav class="navbar-dark">

            <ul class="navbar-nav">
                <li class="nav-item">
                    <a class="nav-link nav-header" href="#">Pending Tasks</a>
                </li>
                <li class="todo-item" v-for="todo in todos" v-show="!todo.done">{{todo.title}}</li>

                <li class="nav-item">
                    <a class="nav-link nav-header" href="#">Completed Tasks</a>
                </li>
                <li class="todo-item" v-for="todo in todos" v-show="todo.done">{{todo.title}}</li>
            </ul>
        </nav>
    </aside>

</template>
<script>


    export default {
        props: ['todos'],
        methods: {
            trigger(){
                console.log('ddd')
            }
        }

    }

</script>

<style scoped lang="less">
    @import (reference) '../../assets/less/mainstyles.less';

    .navbar-body {
        background-color: @grey;
        padding: 0;
        height: 150vh;
        width: 305px;

        .navbar-nav {

            background-color: @white;
            padding: 0 0 20px 0;
            border-right: @yellow 3px solid;

            .todo-item {
                font-size: 16px;
                font-weight: bold;
                padding: 0 0 0 30px;
            }

            .new-task-button {
                background-color: @yellow;
                color: @white;
                font-size: 40px;
                font-weight: bolder;
                border: none;
                text-align: left;
                padding: 0 0 0 30px;
                height: 100px;
                cursor: pointer;
            }

            .nav-header {
                font-size: 24px;
                padding: 20px 0 20px 0;
            }
            span {
                color: @yellow;
                display: inline-block;
            }

            .nav-item {
                font-size: 20px;
                font-weight: bold;
                padding: 0 0 0 30px;

            }
        }
    }

    .navbar-dark .navbar-nav .nav-link {
        color: #000;

        &:hover {
            color: @yellow;

        }
    }


</style>