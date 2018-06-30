<template>
    <div>
        <task-toggle :todosCount="todos.filter(todo => {return todo.done === false}).length"
                     title="Pending Tasks"></task-toggle>

        <div v-if="todos.filter(todo => {return todo.done === true})"></div>
        <div class="row">

            <todo v-on:delete-todo="deleteTodo" v-on:complete-todo="completeTodo" v-for="todo in todos"
                  :todo.sync="todo" :key="todo.id" v-show="!todo.done"></todo>
        </div>
        <task-toggle :todosCount="todos.filter(todo => {return todo.done === true}).length" class="taskCompleted"
                     title="Completed Tasks"></task-toggle>

        <div class="row">
            <todo v-on:delete-todo="deleteTodo" v-on:complete-todo="completeTodo" v-for="todo in todos"
                  :todo.sync="todo" :key="todo.id" v-show="todo.done"></todo>
        </div>
    </div>
</template>

<script type="text/javascript">
    import Todo from './Todo';
    import TaskToggle from './TaskToggle.vue'


    export default {
        props: ['todos'],
        components: {
            Todo,
            TaskToggle
        },
        methods: {
            deleteTodo(todo) {
                const todoIndex = this.todos.indexOf(todo);
                this.todos.splice(todoIndex, 1);

            },
            completeTodo(todo) {
                const todoIndex = this.todos.indexOf(todo);
                this.todos[todoIndex].done = true;
            },
        }
    };
</script>

<style scoped>

</style>

