<script setup>
import {ref, watch} from 'vue'
let todos = ref(JSON.parse(window.localStorage.getItem('todos'))?? [])
let newTodo = ref([])
let input = ref('')
let filter = ref('')


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
 
function activeFilter (todo) {
  return todo.complete == false
}


function todofilter (todo) {
  if (filter.value == 'incompleted')
  { return todo.complete == false}    
  else if(filter.value == "completed"){
    return todo.complete == true 
  } 
  else{return true}
  }


  watch(todos, function(value) {
      window.localStorage.setItem('todos', JSON.stringify(value))
    }, {deep: true})
</script>

<template>
  <img  class="img" src="list.png" alt="Todo List">
<body>

  <h2> {{ todos.filter(activeFilter).length }} Items left!</h2>
<input v-model="newTodo" @keydown.enter="addTodo">
<button @click="addTodo">Add Todo</button><hr>

<p v-if="todos.length >0">  
  <input name="filter" type="radio" value="all" v-model="filter">
<label>All</label>

<input name="filter" type="radio" value="completed" v-model="filter">
<label>Completed</label>

<input name="filter" type="radio" value="incompleted" v-model="filter">
<label>Incompleted</label>
<hr>

</p>

  <li v-for="(todo, index) in todos.filter(todofilter)">

    <input type="checkbox" v-model="todo.complete">

{{todo.text}}


<button @click="deleted(index)">Delete</button><hr>
<P v-for="todo in todos" v-if="filter == 'active' && todo.complete == false" >{{ todo.text }}</P>
  </li>




</body>
</template>

<style scoped>
 

body{
font-style: italic;
text-align: center;
background-color: rgb(56, 50, 50);
color: rgb(0, 242, 255);
font-size: medium;
}
  
button{ 
width:100px;
height: 50px;
background-color: rgb(120, 118, 121);
color: rgb(207, 207, 207);
font-size: large;}

button:hover{
color: rgb(255, 0, 0);
font-size: large;
background-color: rgb(29, 226, 229);}
template{
  background-color: black;
}

h1{
font-size: 45px;    
text-align: center;
color: aquamarine;
}

h2{
font-size: 40px;
color: rgb(0, 221, 255);
}

p{
font-size: 20px;
}
.img{

  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 25%;
}

</style>
