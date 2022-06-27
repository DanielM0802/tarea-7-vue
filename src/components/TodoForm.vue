<template>
  <form @submit.prevent="anadirTodo(todo)">
    <input v-model="todo" type="text" placeholder="¿Qué quieres hacer hoy?..." /><button>➕</button>
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
  async mounted(){
    const url = 'http://www.boredapi.com/api/activity/';
    let response = await fetch(url).then(res => res.json());
    console.log(response)
    this.anadirTodo(response.activity);
  }
};
</script>

<style scoped>
  form{
    margin: 20px 0;
  }
  input{
    width: 60%;
    border-radius: 4px;
    font-size: 20px;
    padding: 5px 5px;
  }
  button{
    font-size: 20px;
    border-radius: 50%;
    margin-left: 10px;
  }
  button:hover{
    cursor: pointer;
  }
</style>
