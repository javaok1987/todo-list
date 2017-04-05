<style lang="scss">

#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}

h1,
h2 {
    font-weight: normal;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    display: inline-block;
    margin: 0 10px;
}

a {
    color: #42b983;
}

.completed {
    text-decoration: line-through;
}

</style>

<template>

<div id="app">
    <img src="./assets/logo.png" width="64">
    <h1>{{title}}</h1>
    <h2>{{describe}}</h2>
    <input type="text" autofocus v-model="newTask" @keyup.enter="add" />
    <button @click="add">Add Todo</button>
    <button @click="clearList">Clear List</button>
    <div class="">
        <ul v-for="(task, idx) in tasks">
            <li>
                <input type="checkbox" class="checkbox" v-model="task.completed">
                <span :class="{completed: task.completed}">{{task.title}}</span>
                <button type="button" name="button" @click="remove(idx)">delete</button>
                <!-- <button type="button" name="button" @click="complete(idx)">Complete</button> -->
            </li>
        </ul>
    </div>
</div>

</template>

<script>

class Task {
    constructor(title) {
        this.title = title;
        this.completed = false;
    }
}

export default {
    name: 'app',
    data() {
        return {
            title: 'Hello Vue.js',
            describe: 'A simple todo list application built with Vue.js',
            tasks: [{
                title: 'task 1',
                completed: false

            }, {
                title: 'task 2',
                completed: false
            }, {
                title: 'task 3',
                completed: false
            }],
            newTask: ''
        }
    },
    components: {},
    methods: {
        add: function() {
            var task = this.newTask.trim();
            if (task) {
                this.tasks.push(new Task(this.newTask))
                this.newTask = ''
            }
        },
        remove: function(idx) {
            this.tasks.splice(idx, 1)
        },
        complete: function(idx) {
            this.tasks[idx].completed = true
        },
        clearList: function() {
            this.tasks = []
        }
    }
}

</script>
