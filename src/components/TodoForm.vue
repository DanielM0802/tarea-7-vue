<template>
  <form @submit.prevent="anadirTodo(todo)">
    <input v-model="todo" type="text" /><button>Añadir</button>
  </form>
</template>

<script>
import { ref } from "vue";
import { useTodoListStore } from "../store/useTodoListStore";
export default {
  setup() {
    const todo = ref("");
    const store = useTodoListStore();

    function anadirTodo(item) {
      if (item.length === 0) {
        return;
      }
      store.addTodo(item);
      todo.value = "";
    }

    return { todo, anadirTodo };
  },
};
</script>

<style lang="scss" scoped></style>
