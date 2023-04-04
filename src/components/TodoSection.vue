<template>
  <div id="todoSection" class="px-3 bg-slate-500 w-1/3 rounded-md py-3">
    <TodoSectionHead/>
    <todo-section-buttons/>
    <todo-section-body/>
  </div>
</template>

<script>
import TodoSectionHead from './TodoSectionHead.vue'
import TodoSectionButtons from './TodoSectionButtons.vue'
import TodoSectionBody from './TodoSectionBody.vue'

export default {
    components : {TodoSectionHead,TodoSectionButtons,TodoSectionBody}
  
}
</script>