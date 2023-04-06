<template>
  <div class="scroll-auto overflow-hidden">
  <todo-card></todo-card>
  <todo-card></todo-card>
  <todo-card></todo-card>
  <todo-card></todo-card>
  <todo-card></todo-card>
</div>
</template>

<script>
import TodoCard from './TodoCard.vue'

export default {
 components : {TodoCard}
}
</script>