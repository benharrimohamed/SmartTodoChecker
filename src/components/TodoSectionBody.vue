<template>
  <div>
    <TodoAddTaskForm></TodoAddTaskForm>
    <Todos></Todos>
  </div>
</template>

<script>
import TodoAddTaskForm from './TodoAddTaskForm.vue'
import Todos from './Todos.vue'
export default {
    components: {TodoAddTaskForm,Todos}

}
</script>
