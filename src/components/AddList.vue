<script setup>
import { defineProps, ref,defineEmits } from 'vue'
const todo = ref('')
const props = defineProps({
    addlist:{
        type: Array,
        required: true
    }
    })
const emits = defineEmits(['add'])
const add = () => {
    if(todo.value.trim() !== ''){
        emits("add",{
            id: Date.now(), 
            content: todo.value,
            completed: false 
        })
    todo.value = ''
    }
    
}
</script>

<template>
<div class="input-group mb-3">
  <input type="text" class="form-control" placeholder="请添加数据" aria-label="Recipient's username" aria-describedby="button-addon2" v-model="todo">
  <button class="btn btn-outline-secondary" type="button" id="button-addon2" @click="add">添加</button>
</div>
</template>

<style scoped>
.form-control{
    width: 300px;
}
</style>