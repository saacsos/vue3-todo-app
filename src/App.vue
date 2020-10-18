<template>
  <h1>Vue 3 Todo App</h1>

  
  <form @submit.prevent="addNewTodo">
    <label>New Todo</label>
    <input v-model="newTodo" type="text" name="newTodo">
    <button>Add New Todo</button>
  </form>

    <button @click="markAllDone">Mark All Done</button>


  <ul>
    <li v-for="(todo, index) in todos" :key="todo.id" class="todo-item">
      <span :class="{ done: todo.done }" @click="toggleDone(todo)">
        {{ todo.content }}
      </span> 
      <button @click="removeTodo(index)">Remove</button>
    </li>
  </ul>

  <hr>
  <hello-world></hello-world>
</template>

<script>
import { ref, onMounted } from 'vue'
import HelloWorld from '@/components/HelloWorld'

export default {
  components: {
    HelloWorld
  },
  
  

  setup() {
    const newTodo = ref('')
    const todos = ref([])

    onMounted(() =>{
      todos.value.push({
        id: Date.now(),
        done: false,
        content: 'Learn Vue 3'
      })
    })

    function addNewTodo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      })
      newTodo.value = ''
    }

    function toggleDone(todo) {
      todo.done = !todo.done
    }

    function removeTodo(index) {
      todos.value.splice(index, 1)
    }

    function markAllDone() {
      todos.value.forEach((todo) => todo.done = true)
    }

    return {
      newTodo,
      todos,
      addNewTodo,
      toggleDone,
      removeTodo,
      markAllDone
    }

    
    
  }
}
</script>

<style>

.done {
  text-decoration: line-through;
}

.todo-item {
  cursor: pointer;
}
</style>
