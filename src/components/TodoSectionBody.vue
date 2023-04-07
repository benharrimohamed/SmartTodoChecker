<template>
  <div>
    <TodoSectionButtons v-if="isAddingNewTodo"></TodoSectionButtons>
    <TodoAddTaskForm></TodoAddTaskForm>
    <Todos></Todos>
  </div>
</template>

<script>
import TodoAddTaskForm from './TodoAddTaskForm.vue'
import Todos from './Todos.vue'
import TodoSectionButtons from './TodoSectionButtons.vue';
export default {
    components: {TodoSectionButtons,TodoAddTaskForm,Todos},
    setup (props) {
      const isAddingNewTodo = props.isAddingNewTodo

      return {
        isAddingNewTodo
      }
    }

}
</script>
