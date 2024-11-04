<script setup>
import { ref, computed, defineProps, defineEmits } from 'vue';

const props = defineProps({
  todolist: {
    type: Array,
    required: true
  }
});
// 定义事件
const emits = defineEmits(['filter'])
// 高亮变量
const activeButton = ref('all')

const filterList = computed(() => {
  return props.todolist.filter(item => item.completed)
})

const noFilterList = computed(() => {
  return props.todolist.filter(item => !item.completed)
})

const setActiveButton = (button) => {
  activeButton.value = button
  switch (button) {
    case 'all':
      emits('filter', props.todolist);
      break;
    case 'completed':
      emits('filter', filterList.value);
      break;
    case 'notCompleted':
      emits('filter', noFilterList.value);
      break;
  }
};
</script>

<template>
  <!-- 按钮组 -->
  <div class="btn-group" role="group" aria-label="Basic example">
    <button
      type="button"
      class="btn"
      :class="{ 'btn-primary': activeButton === 'all', 'btn-outline-primary': activeButton !== 'all' }"
      @click="setActiveButton('all')"
    >
      全部
    </button>
    <button
      type="button"
      class="btn"
      :class="{ 'btn-primary': activeButton === 'completed', 'btn-outline-primary': activeButton !== 'completed' }"
      @click="setActiveButton('completed')"
    >
      已完成
    </button>
    <button
      type="button"
      class="btn"
      :class="{ 'btn-primary': activeButton === 'notCompleted', 'btn-outline-primary': activeButton !== 'notCompleted' }"
      @click="setActiveButton('notCompleted')"
    >
      未完成
    </button>
  </div>
</template>

<style scoped>
.btn-group {
  width: 400px;
  margin: 20px auto;
}
/* 高亮状态 */
.btn-primary {
  background-color: #007bff; 
  color: white; 
}
/* 未高亮状态 */
.btn-outline-primary {
  background-color: white;
  color: #007bff;
  border: 1px solid #007bff
}
</style>
