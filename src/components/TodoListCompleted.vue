<template>

  <div class="contenedor-lista">
    <button @click="onClick()">Completadas</button>
      <div v-if="mostrarListado" class="listado">
        <div v-for="todo in todoList" :key="todo.id" v-bind:id="todo.id">
          <div v-if="todo.completed" class="row-container" @mouseenter="cambiarVisibilidad(true, todo.id)" @mouseleave="cambiarVisibilidad(false, todo.id)">
            <span :class="{ completed: todo.completed }">{{ todo.item }}</span>
            <div class="botones" v-if="mostrarBotones(todo.id)">
              <span @click.stop="toggleCompleted(todo.id)" >⏫</span>
              <span @click="deleteTodo(todo.id)" class="x">❌</span>
              </div>
          </div>
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
      mostrarListado: false,
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
    },
    onClick(){
      this.mostrarListado = !this.mostrarListado;
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

<style scoped>
.completed {
  text-decoration: line-through;
}
.row-container{
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px 0;
    margin: 10px 0;
    background-color: #e1e1e1;
}
.contenedor-lista{
  width: 80%;
  margin: 0 auto;
  font-size: 20px;
  padding: 20px 0;
  color: red;
}
.botones{
  font-size: 26px;
}
.botones:hover{
  cursor: pointer;
}
</style>
