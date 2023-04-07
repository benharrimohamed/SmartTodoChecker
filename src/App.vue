<template>
    <div class="grid grid-rows-3 m-3 p-4 px-3 border border-red-300 md:grid md:grid-cols-2 lg:grid lg:grid-cols-3 xl:grid-cols-4">
      <todo-section></todo-section>
      <todo-section></todo-section>
      <todo-section></todo-section>
      <todo-section></todo-section>
    </div>
</template>

<script>
import { ref } from 'vue'
import TodoSection from './components/TodoSection.vue'


export default {
  components: { TodoSection }
  
}
</script>
