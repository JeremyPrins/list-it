<template>
    <aside class="sidebar-container col-6 col-md-2">
        <div class="sidebar-content">

            <div class="side-item">
                <p>Pending Tasks</p>
                <ul>
                <li v-for="todo in todos" v-show="!todo.done">{{todo.title}}</li>
                </ul>
            </div>

            <div class="side-item">
                <p>Completed Tasks</p>
                <ul>
                <li class="todo-item-done" v-for="todo in todos" v-show="todo.done">{{todo.title}}</li>
                </ul>
            </div>

        </div>
    </aside>

</template>
<script>


    export default {
        props: ['todos'],
        methods: {
            trigger() {
                console.log('ddd')
            }
        }

    }

</script>

<style scoped lang="less">
    @import (reference) '../../assets/less/mainstyles.less';

    .sidebar-container {
        background-color: @grey;

        padding: 0;
        height: auto;
        border-right: @primaryColor 3px solid;

        .sidebar-content {
            background-color: @white;
            padding: 0 0 20px 40px;

            li {

                font-size: 16px;
                font-weight: bold;
                padding-left: 50px;
            }
            .todo-item-done {
                text-decoration: line-through;
                color: @grey;
            }

            span {
                color: @primaryColor;
                display: inline-block;
            }

            .side-item {

                p {
                    font-weight: bold;
                    padding-top: 20px;
                    font-size: 24px;
                    border-bottom: 3px solid @primaryColor;
                    margin: 0 20px 0 0;
                }
                li {
                    padding-left: 10px;
                    padding-top: 5px;
                }

            }
        }
    }

    .navbar-nav .nav-link {
        color: #000;

    }


</style>