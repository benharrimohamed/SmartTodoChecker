<template>
  <div class="mx-auto">
    <div class="flex mt-6 py-8 px-3 max-h-screen">
      <todo-section></todo-section>
      <todo-section></todo-section>
      <todo-section></todo-section>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'
import TodoSection from './components/TodoSection.vue'


export default {
  components: { TodoSection }
  
}
</script>
