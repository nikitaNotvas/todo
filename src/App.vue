<script setup>
import {ref, watch} from 'vue'
let todos = ref(JSON.parse(window.localStorage.getItem('todos'))?? [])
let newTodo = ref([])
let input = ref('')


function addTodo () {
todos.value.push({
	text: newTodo.value,
	complete: false,

})
	newTodo.value = ('')
}
function deleted(index) {
  todos.value.splice(index, 1)
}

function todofilter (todo) {
  if (filter.value == 'active'){ return todo.complete == false}    
  else{ 
    return true
   } 
  }


  watch(todos, function(value) {
      window.localStorage.setItem('todos', JSON.stringify(value))
    }, {deep: true})
</script>

<template>
  <h1>My Todo Application</h1>
<body>
  <input name="filter" type="radio" value="all" v-model="filter">
<label>All</label>
<input name="filter" type="radio" value="active" v-model="filter">
<label>Active</label><br><hr>

  <li v-for="(todo, index) in todos">

    <input type="checkbox" v-model="todo.complete">

{{todo.text}}

<button @click="deleted(index)">Delete</button><hr>
<P v-for="todo in todos" v-if="filter == 'active' && todo.complete == false">{{ todo.text }}</P>
  </li>
  <input v-model="newTodo" @keydown.enter="addTodo">
  <button @click="addTodo">Add Todo</button>




</body>
</template>

<style scoped>
 

body{
font-style: italic;
text-align: center;
background-color: rgb(56, 50, 50);
color: rgb(44, 138, 0);
}
  
button{ 
width:100px;
height: 50px;
background-color: rgb(115, 0, 153);
color: rgb(255, 0, 0);
font-size: large;}

button:disabled{
color: rgb(255, 0, 0);
background-color: rgb(0, 0, 0);
font-size: large;
}

button:hover{
color: rgb(255, 0, 0);
font-size: large;
background-color: rgb(7, 108, 2);}
  

button{color: #000;
}
h1{
font-size: 45px;    
}

h2{
font-size: 40px;
color: rgb(255, 255, 255);
}

p{
font-size: 30px;
}

</style>
