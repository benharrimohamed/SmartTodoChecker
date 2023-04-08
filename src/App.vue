<template>
    <div class="grid m-3 p-4 border border-red-300">
      <div class="mx-auto w-full border-red-300 p-2 rounded-md shadow-md bg-blue-500 md:max-mx-1/3">
        <div class="flex justify-between">
         <div class="text-white font-bold">Todos</div>
         <div>
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6 text-white">
           <path stroke-linecap="round" stroke-linejoin="round" d="M6.75 12a.75.75 0 11-1.5 0 .75.75 0 011.5 0zM12.75 12a.75.75 0 11-1.5 0 .75.75 0 011.5 0zM18.75 12a.75.75 0 11-1.5 0 .75.75 0 011.5 0z" />
          </svg>
        </div>
       </div>
       <div>
        <button class="bg-white py-1 w-full rounded-md mt-2" @click="handleAddingButtonEvent">

          <svg v-if=isAddingTodo xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" 
          stroke-width="1.5" stroke="currentColor" class="w-6 h-6 mx-auto text-red-500">
          <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
          </svg>

          <svg v-else xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" 
          stroke-width="1.5" stroke="currentColor" class="w-6 h-6 mx-auto text-blue-500">
          <path stroke-linecap="round" stroke-linejoin="round" d="M12 4.5v15m7.5-7.5h-15" />
          </svg>

        </button>
       </div>
       <TodoAddTaskForm v-if=isAddingTodo></TodoAddTaskForm>
       <div v-else 
              v-for="todo in state.todos" :key="todo.id">
        <TodoCard :todo=todo ></TodoCard>
       </div>
     </div>
   </div>
</template>

<script>
import TodoCard from './components/TodoCard.vue';
import TodoAddTaskForm from './components/TodoAddTaskForm.vue';
import { onBeforeMount, reactive, ref } from 'vue';

export default {
  components : {
    TodoCard,
    TodoAddTaskForm
  },
  setup () {

      const isAddingTodo = ref(false)
      const state = reactive({todos : []})
      const handleAddingButtonEvent = () => {isAddingTodo.value=!isAddingTodo.value}

      const getTodosFromApi = async () => {
        fetch("http://localhost:3000/todos")
        .then(res => res.json())
        .then(data => state.todos = data)
        .catch (err => console.log(err))
      }

      onBeforeMount (() => {
        getTodosFromApi()
      })

      return {
        isAddingTodo,
        handleAddingButtonEvent,
        state
      }
  }
}
</script>
