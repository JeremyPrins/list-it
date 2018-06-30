<template>
    <div>
        <!-- Button to Open the Modal -->
        <button class="btn" data-toggle="modal" data-target="#newTaskModal" data-backdrop="static"
                data-keyboard="false" v-on:click="openForm">New Task
        </button>

        <!-- The Modal -->
        <div class="modal" id="newTaskModal">
            <div class="modal-dialog">
                <div class="modal-content">

                    <!-- Modal Header -->
                    <div class="modal-header">
                        <h4 class="modal-title">New Task</h4>
                        <button type="button" class="close" data-dismiss="modal" v-on:click.prevent="closeForm">
                            &times;
                        </button>
                    </div>

                    <!-- Modal body -->
                    <div class="modal-body" v-show="isCreating">
                        <form>
                            <div class="form-group">
                                <label for="Title">Title</label>
                                <input class="form-control" v-model="title" type='text' id="Title" name="Title"
                                       maxlength="20" placeholder="Task Title ..." autofocus>
                            </div>
                            <div class="form-group">
                                <label for="Description">Description</label>
                                <textarea class="form-control" rows="2" v-model="description" id="Description"
                                          maxlength="100" placeholder="Task Description ..."></textarea>
                            </div>
                            <div class="form-group">
                                <label>Subtasks</label>
                                <input class="form-control" v-model="subtasks[0].name" type='text' id="Subtasks1"
                                       name="Subtasks"
                                       maxlength="20" placeholder="Subtask 1 ...">
                                <br>

                                <input class="form-control" v-model="subtasks[1].name" type='text' id="Subtasks2"
                                       name="Subtasks"
                                       maxlength="20" placeholder="Subtask 2 ...">
                                <br>
                                <input class="form-control" v-model="subtasks[2].name" type='text' id="Subtasks3"
                                       name="Subtasks"
                                       maxlength="20" placeholder="Subtask 3 ...">
                                <br>
                                <input class="form-control" v-model="subtasks[3].name" type='text' id="Subtasks4"
                                       name="Subtasks"
                                       maxlength="20" placeholder="Subtask 4 ...">
                            </div>
                            <div class="form-group">
                                <label for="Location">Location</label>
                                <input class="form-control" v-model="location" type='text' id="Location"
                                       name="Location" placeholder="Task Location  ...">
                            </div>
                            <div class="form-group">
                                <label for="Deadline">Deadline</label>
                                <input class="form-control" v-model="deadline" type='text' id="Deadline"
                                       name="Deadline" placeholder="Task Deadline ...">
                            </div>

                            <div class="form-group">
                                <label for="Category">Category</label>
                                <input class="form-control" v-model="category" type='text' id="Category"
                                       name="Category" placeholder="Task Category ...">
                            </div>


                        </form>
                    </div>

                    <!-- Modal footer -->
                    <div class="modal-footer">

                        <button type="submit" class="btn" data-dismiss="modal"
                                v-on:click.prevent="sendForm() || closeForm()">Create Task
                        </button>
                        <button type="button" class="btn" data-dismiss="modal"
                                v-on:click.prevent="closeForm">Close Form
                        </button>
                    </div>

                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {


        data() {

            return {
                title: '',
                description: '',
                subtasks: [{
                    name: '',
                    completed: false
                }, {
                    name: '',
                    completed: false
                }, {
                    name: '',
                    completed: false
                }, {
                    name: '',
                    completed: false
                }],
                location: '',
                deadline: '',
                category: '',
                isCreating: false,
            };
        },
        methods: {

            openForm() {
                this.isCreating = true;
            },
            closeForm() {
                this.isCreating = false;
            },

            sendForm() {
                const title = this.title;
                const description = this.description;
                const subtasks = this.subtasks;
                const location = this.location;
                const deadline = this.deadline;
                const category = this.category;

                if (title.length && description.length && deadline.length && category.length > 0) {

                    this.$emit('create-todo', {
                        title,
                        description,
                        subtasks,
                        location,
                        deadline,
                        category,
                        done: false,
                    });

                    this.title = '';
                    this.description = '';
                    this.subtasks = [{
                        name: '',
                        completed: false
                    }, {
                        name: '',
                        completed: false
                    }, {
                        name: '',
                        completed: false
                    }, {
                        name: '',
                        completed: false
                    }];
                    this.location = '';
                    this.deadline = '';
                    this.category = '';
                    this.isCreating = false;

                } else {
                    document.getElementsByName('Title')[0].placeholder = 'This field is empty';

                }

            }
        }
    };
</script>

<style scoped lang="less">
    @import (reference) '../assets/less/mainstyles.less';

    .btn {
        margin-top: 20px;
        margin-left: 20px;
        color: @white;
    }

    .new-task-form {
        margin: 20px;
        padding: 10px;
        border: @primaryColor 3px solid;
    }

    .modal-dialog {
        max-width: 400px;

        .modal-content {
            padding: 30px;

            .modal-footer {
                button {
                    background-color: @primaryColor;
                    color: @white;
                }

            }
        }
    }


</style>