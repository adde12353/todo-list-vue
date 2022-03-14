<template>
  <h1>Att göra lista</h1>
  <form @submit.prevent="btn" >
    
  <input type="text" placeholder="Saker du vill göra" v-model="name">
  <button>Lägg till</button>
  </form>

  <div class="todo-item" v-for="(todo, index) in todos" :key="todo.id">
    <h2 :class="{ done: todo.done }" class="todo-text">{{todo.cont}}</h2>
    <button @click="toggleDone(todo)">Klar!</button>
    <button @click="remove(index)">Ta bort</button>
  </div>
</template>


<script>
import { ref } from 'vue'

export default{
  setup(){
    const name = ref("")
    const todos = ref([]);

    const btn = () => {
      todos.value.push({
        id: Date.now(),
        done: false,
        cont: name.value,
      });
      name.value="";
    }

    function toggleDone(todo){
      todo.done = !todo.done;
    }

    function remove(index){
      todos.value.splice(index, 1)
    }

    return {
     btn, name, todos, toggleDone, remove,
    }
  },
}
</script>

<style>
body{
  background-color: rgb(4, 4, 61);
  color: aliceblue;
}
input, button{
  font-size: 20px;
}
.todo-text{
  min-width: 93px;
}
.todo-item{
  text-align: center;
}
button{
  min-width: 77.15px
}
.done{ text-decoration: line-through;
text-decoration-color: black
; 
}
.todo-text{margin-right: 15px;}
.todo-item{display: flex; align-items: center; justify-content: center;}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 60px;
}
</style>
