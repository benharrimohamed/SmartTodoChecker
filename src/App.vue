<template>
  <div class="mx-auto">
    <div class="flex mt-6 p-3">
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
