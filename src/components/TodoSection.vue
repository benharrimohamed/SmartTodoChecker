<template>
  <div id="todoSection" class="mb-2 p-3 max-h-screen border border-red-300 mx-1 rounded-lg shadow-md bg-slate-500">
    <TodoSectionHead></TodoSectionHead>
    <TodoSectionBody :isAddingNewTodo="isAddingNewTodo"></TodoSectionBody>
  </div>
</template>

<script>
import TodoSectionHead from './TodoSectionHead.vue'
import TodoSectionButtons from './TodoSectionButtons.vue'
import TodoSectionBody from './TodoSectionBody.vue'
import { ref } from 'vue'

export default {
    components : {TodoSectionHead,TodoSectionButtons,TodoSectionBody},
    setup () {
      const isAddingNewTodo = ref(false)

    }
  
}
</script>