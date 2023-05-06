<template>
    <div>
      <h1>Todo List</h1>
      <ul>
        <li v-for="todo in todos" :key="todo.id">
        {{ todo.title }}
        </li>
      </ul>
      <create-todo @new-todo="addNewTodo"></create-todo>
    </div>
</template>
<script>
    import { ref } from "vue";
    import CreateTodo from "./CreateTodo.vue";

    export default {
    components: {
        CreateTodo,
    },
    data() {
        console.log(this.title)
        const todos = ref([]);
        return { todos };
    },
    methods: {
        addNewTodo (newTodo) {
            this.todos.push(...newTodo); // update todos with new todo data
        }
    },
    onMounted() {
        const storedTodos = localStorage.getItem("todos");
        if (storedTodos) {
            this.todos = JSON.parse(storedTodos);
        }
    },
  };
   
</script>
  