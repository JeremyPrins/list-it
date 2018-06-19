<template>
    <transition name="slide-fade">
        <div class="col-sm-3 task-card" v-bind:class="{ taskCompleted : todo.done}">
            <div class="card">
                <a class="card-header">
                    <h5 class="card-title"><i class="far fa-check-circle"></i> {{ todo.title }}</h5>
                    <div v-show="!isEditing && !todo.done"></div>
                    <div v-show="!isEditing &&todo.done" disabled></div>
                </a>


                <div class="card-body" v-show="!isEditing">
                    <div v-show="!todo.description == ''">
                        <p><i class="far fa-comment-alt"></i>

                            {{ todo.description }}</p>
                        <hr>
                    </div>

                    <div v-show="!todo.subtasks == []">
                        <i class="fas fa-tasks"></i>
                        <ol>
                            <li v-for="(tasks, index) in todo.subtasks" v-show="!tasks.name == ''" >
                                <input v-show="!todo.done" :id="index + todo.title" type="checkbox"
                                       :checked="tasks.completed"><label
                                    :for="index + todo.title">{{tasks.name}}</label>
                            </li>
                        </ol>

                        <hr>
                    </div>

                    <div v-show="!todo.location == ''">
                        <p><i class="fas fa-map-marker"></i>{{ todo.location }}</p>
                        <hr>
                    </div>
                    <div v-show="!todo.deadline == ''">
                        <p><i class="far fa-calendar"></i> {{ todo.deadline }}</p>
                        <hr>
                    </div>

                    <div v-show="!todo.category == ''">
                        <p><i class="far fa-star"></i>{{ todo.category }}</p>
                        <hr>
                    </div>

                    <span class="btn" v-on:click="showForm" v-show="!todo.done"> Edit Todo </span>
                    <span class="btn" v-on:click="deleteTodo(todo)" v-show="todo.done"> Delete Todo </span>
                    <span class="btn" v-on:click="completeTodo(todo)" v-show="!isEditing && !todo.done"> Complete</span>


                </div>
            </div>

            <div v-show="isEditing">
                <div class="card">
                    <div class="editForm">
                        <div class="form-group">
                            <label for="Title">Title</label>
                            <input class="form-control" v-model="todo.title" type='text' id="Title" name="Title"
                                   maxlength="20">
                        </div>
                        <div class="form-group">

                            <label for="Description">Description</label>
                            <textarea class="form-control" v-model="todo.description" id="Description"
                                      maxlength="100"></textarea>
                        </div>
                        <div class="form-group" v-for="(tasks, index) in todo.subtasks">

                            <label for="Subtasks">Subtask {{index + 1}}</label>
                            <input class="form-control" v-model="tasks.name" type='text' id="Subtasks" name="Subtasks"
                                   maxlength="20">
                        </div>
                        <div class="form-group">

                            <label for="Location">Location</label>
                            <input class="form-control" v-model="todo.location" type='text' id="Location"
                                   name="Location">
                        </div>
                        <div class="form-group">
                            <label for="Deadline">Deadline</label>
                            <input class="form-control" v-model="todo.deadline" type='text' id="Deadline"
                                   name="Deadline">
                        </div>
                        <div class="form-group">

                            <label for="Category">Category</label>
                            <input class="form-control" v-model="todo.category" type='text' id="Category"
                                   name="Category">
                        </div>
                        <button class='btn' v-on:click="hideForm">
                            Complete edit
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </transition>
</template>

<script type="text/javascript">
    export default {
        props: ['todo'],
        data() {
            return {
                isEditing: false,
            };
        },
        methods: {
            completeTodo(todo) {
                this.$emit('complete-todo', todo);
            },
            deleteTodo(todo) {
                this.$emit('delete-todo', todo);
            },
            showForm() {
                this.isEditing = true;
            },
            hideForm() {
                this.isEditing = false;
            },

        },
    };
</script>

<style scoped lang="less">
    @import (reference) '../assets/less/mainstyles.less';

    .completed {
        text-decoration: line-through;
        color: #bababa;

    }


    .editForm{
        padding: 20px;
    }

    .task-card {
        padding: 20px;
        display: inline-block;
        transition: all 1s;

        .card {
            border: @yellow 2px solid;
            box-shadow: 10px 6px 30px 0 rgb(168, 168, 168);
            .card-body {

                div {

                    display: inline;

                    p {
                        font-size: 16px;
                    }

                    i {
                        padding-right: 20px;
                    }
                }

                ol {

                    li {
                        font-size: 16px;
                        font-weight: normal;

                    }
                }
                input {
                    margin-right: 10px;
                    margin-left: 10px;
                    &[type=checkbox]:checked + label {
                        text-decoration: line-through;
                        color: #bababa;
                    }
                }
            }
            .btn {
                color: @white;

            }
            .card-header {
                background-color: @yellow;

                .card-title {
                    font-size: 24px;
                    font-weight: bolder;
                    color: @white;
                    padding-top: 10px;
                    text-align: center;
                }
            }
        }

    }

    .slide-fade-enter-active {
        transition: all .3s ease;
    }

    .slide-fade-leave-active {
        transition: all .5s ease;
    }

    .slide-fade-enter, .slide-fade-leave-to {
        opacity: 0;
    }

    .far, .fas {
        padding-right: 20px;
    }
</style>
