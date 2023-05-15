<script setup>
import {ref} from 'vue'
let todos = ref(['','',''])

function addTodo () {
todos.value.push({
	text: newTodo.value,
	complete: false
})
	newTodo.value = ''
}







</script>

<template>
  <h1>My Todo Application</h1>
  <li v-for="todo in todos">
<input type="checkbox" v-model="todo.complete">

{{todo.text}}

<button @click="delete">Delete</button>

  </li>
  <input v-model="newTodo">
  <button @click="add">Add Todo</button>
</template>

<style scoped>

</style>
