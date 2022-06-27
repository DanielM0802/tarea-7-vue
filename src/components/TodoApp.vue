<template>
  <div class="contenedor">
    <h1>Todoer</h1>
    <todo-form />
    <todo-list />
    <TodoListCompleted />
  </div>
</template>

<script>
import TodoForm from "./TodoForm.vue";
import TodoList from "./TodoList.vue";
import TodoListCompleted from "./TodoListCompleted.vue";
export default {
  components: { TodoForm, TodoList, TodoListCompleted },
  setup() {
    return {};
  },
};
</script>

<style scoped>
  .contenedor{
    width: 70%;
    margin: 0 auto;
    border: 1px solid black;
  }
  h1{
    margin: 0;
    text-align: left;
    border-bottom: 1px solid black;

  }
</style>
