<script setup>
import { ref, onMounted } from "vue"
import todoList from "./components/todoList.vue"
import FliterButton from "./components/FliterButton.vue"
import AddList from "./components/AddList.vue"
// 初始数据
const todos = ref([])
// 过滤后的数据
const filteredTodos = ref([])
// 获取远程 todos
const fetchTodos = async () => {
  const response = await fetch(
     "https://jsonplaceholder.typicode.com/todos?_limit=3"
  )
  const rawTodos = await response.json()
  todos.value = rawTodos.map((todo) => ({
    id: todo.id,
    content: todo.title,
    completed: todo.completed,
  }))
  filteredTodos.value = todos.value // 默认显示全部数据
}
// 监听过滤按钮点击事件
const ButtonClick = (data)=>{
  filteredTodos.value = data // 添加数据后立即渲染数据
}
// 挂载后获取远程数据
onMounted(() => {
    fetchTodos()
  })
// 添加数据
const addTodo =(todo)=>{
  todos.value.push(todo)
  filteredTodos.value = todos.value
}
</script>

<template>
  <h1>Todo List</h1>
  <AddList :addlist="todos" @add="addTodo"></AddList>
  <todoList :todolist="filteredTodos"></todoList>
  <FliterButton :todolist="todos" @filter="ButtonClick"></FliterButton>
  
</template>

<style scoped>
</style>
