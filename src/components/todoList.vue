<script setup>
import { ref,defineProps } from 'vue'
const props = defineProps({
    todolist: {
    type: Array,
    required: true
  }
})
</script>

<template>
<ul class="list-group" v-for="todo in todolist" :key="todo.id">
  <li class="list-group-item d-flex justify-content-between align-items-center">
    <!-- 复选框 -->
  <div class="form-check">
  <input class="form-check-input" type="checkbox" value="" :id="todo.id" v-model="todo.completed">
  <label class="form-check-label" :for="todo.id" :class = "{ 'delete': todo.completed }">
    {{ todo.content }}
  </label>
</div>
    <span class="badge text-bg-primary rounded-pill" v-if="todo.completed">已完成</span>
    <span class="badge text-bg-warning rounded-pill" v-else>未完成</span>
  </li>
</ul>
</template>

<style scoped>
.list-group{
    width: 500px;
    margin: 0 auto;
    padding: 10px;
}
.delete{
  text-decoration-line: line-through
}
</style>