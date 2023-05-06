
<template>
    <div>
        <h1>Create Todo</h1>
        <form @submit.prevent="addTodo">
            <label for="title">Title: </label>
            <input type="text" v-model="title" id="title" />
            <button type="submit">Create</button>
        </form>
    </div>
</template>
<script>
import {ref} from "vue";
export default {
    setup() {
        const title = ref('');
        const newTodo = [];
        return {
            title,
            newTodo
        };
    },
    methods: {
        addTodo() {
            const todo = [
                {
                    id: Date.now(),
                    title: this.title,
                    completed: false
                }
            ];
            this.newTodo = todo;
            const todos = JSON.parse(localStorage.getItem('todos')) || [];
            localStorage.setItem('todos', JSON.stringify([...todos, ...todo]));
            this.title = '';
            this.$emit('new-todo', todo);
        },

    }
};
</script>