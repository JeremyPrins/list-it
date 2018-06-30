<template>
    <div>
        <top-menu></top-menu>
        <div class="row side-menu">
            <side-menu v-bind:todos="todos"></side-menu>
            <main class="col">
                <create-todo v-on:create-todo="createTodo"></create-todo>

                <todo-list v-bind:todos="todos"></todo-list>
            </main>
        </div>
    </div>
</template>

<script>
    import SideMenu from './components/navigation-components/SideMenu.vue'
    import TopMenu from './components/navigation-components/TopMenu.vue'
    import TodoList from './components/TodoList';
    import CreateTodo from './components/CreateTodo';

    export default {
        name: 'app',
        data() {
            return {
                todos: [{
                    title: 'Stageplek vinden',
                    description: 'Zoeken naar afstudeer stage plekken in Rotterdam',
                    subtasks: [
                        {
                            name: 'Bedrijven mailen en bellen.',
                            completed: false
                        },
                        {
                            name: 'In gesprek gaan met bedrijven.',
                            completed: false
                        },
                        {
                            name: 'Stage opdracht formuleren.',
                            completed: false
                        },
                        {
                            name: 'Goedkeuring school stage.',
                            completed: false
                        }
                    ],
                    location: 'Hogeschool Rotterdam Wijnhaven',
                    deadline: '30-08-2018',
                    category: 'School',
                    done: false,
                }, {
                    title: 'Belastingaangifte',
                    description: 'Belastingaangifte 2017',
                    subtasks:
                        [
                            {
                                name: 'Loonstroken verzamelen.',
                                completed: false
                            },
                            {
                                name: 'Formulieren belasting invullen.',
                                completed: false
                            }

                        ],
                    location: 'Thuis',
                    deadline: '08-08-2018',
                    category: 'Belastingen',
                    done: false,
                }],
            };
        },
        methods: {
            createTodo(newTodo) {
                this.todos.push(newTodo);
            },
        },

        components: {
            TodoList,
            CreateTodo,
            SideMenu,
            TopMenu,
        },
        mounted() {
            if (localStorage.getItem('todos')) this.todos = JSON.parse(localStorage.getItem('todos'));
        },
        watch: {
            todos: {
                handler() {
                    localStorage.setItem('todos', JSON.stringify(this.todos));
                },
                deep: true,
            }
        }
    };
</script>
