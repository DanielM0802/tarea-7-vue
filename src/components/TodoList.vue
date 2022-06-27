<template>
  <div v-for="todo in todoList" :key="todo.id" v-bind:id="todo.id">
    <div class="row-container" @mouseenter="cambiarVisibilidad(true, todo.id)" @mouseleave="cambiarVisibilidad(false, todo.id)">
      <span :class="{ completed: todo.completed }">{{ todo.item }}</span>
      <div class="botones" v-if="mostrarBotones(todo.id)">
        <span @click.stop="toggleCompleted(todo.id)" >✅</span>
        <span @click="deleteTodo(todo.id)" class="x">❌</span>
        </div>
    </div>
  </div>
</template>

<script>
import { useTodoListStore } from "../store/useTodoListStore";
import { storeToRefs } from "pinia";
export default {

  data(){
    return{
        mostrarBoton : {
            id: 1,
            mostrar: false
        }
    }
  },
  methods: {
    cambiarVisibilidad(show, id){
        this.mostrarBoton.id = id;
        this.mostrarBoton.mostrar = show;
    },
    mostrarBotones(id){
        return this.mostrarBoton.id == id && this.mostrarBoton.mostrar;
    }
  },

  setup() {
    const store = useTodoListStore();
    const { todoList } = storeToRefs(store);
    const { toggleCompleted, deleteTodo } = store;
    return { todoList, toggleCompleted, deleteTodo };
  },
  
};
</script>

<style>
.completed {
  text-decoration: line-through;
}
.row-container{
    display: flex;
}
</style>
