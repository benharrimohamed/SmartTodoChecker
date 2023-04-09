<template>
    <div class="grid m-3 p-2 lg:flex max-w-screen">
      <div class="mx-auto w-full max-w-screen h-screen max-h-screen p-2 rounded-md shadow-md bg-blue-500 ">
        <div class="flex justify-between">
         <div class="text-white font-bold">Todos</div>
          <button id="dropdownMenuIconHorizontalButton" data-dropdown-toggle="dropdownDotsHorizontal" data-te-dropdown-toggle-ref aria-expanded="false">
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6 text-white">
           <path stroke-linecap="round" stroke-linejoin="round" d="M6.75 12a.75.75 0 11-1.5 0 .75.75 0 011.5 0zM12.75 12a.75.75 0 11-1.5 0 .75.75 0 011.5 0zM18.75 12a.75.75 0 11-1.5 0 .75.75 0 011.5 0z" />
          </svg>
        </button>
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
       <todoNavBar v-if="!isAddingTodo"
                    :doneCount="doneCount"
                    :healthCount="healthCount" 
                    :workCount="workCount"
                    :studiesCount="studiesCount"
                    :goalsCount="goalsCount"
                    @getTodosBy="handleGetTodosByCategory"
                    :todosNb="todosNb"
                    ></todoNavBar>
       <TodoAddTaskForm v-if=isAddingTodo  @addNewTodo=addTodo></TodoAddTaskForm>
       <div v-else-if="stateTemp.todos.length >0">
       <div class="border border-red">
       <div v-for="todo in stateTemp.todos" :key="todo.id">
        <TodoCard :todo=todo @TodoIsDone=checkTodo @deleteTodo="deleteTodo"></TodoCard>
       </div>
      </div>
      </div>
       <div v-else class="py-2 bg-blue-300 mt-2 rounded-md"> 
       <div class="mx-auto text-blue-600 font-meduim w-fit">
        Nothing here !
      </div>
      </div>
     </div>
   </div>
</template>

<script>
import TodoCard from './components/TodoCard.vue';
import TodoAddTaskForm from './components/TodoAddTaskForm.vue';
import { onBeforeMount, reactive, ref } from 'vue';
import successToast from './components/Toasts/successToast.vue';
import todoNavBar from './components/todoNavBar.vue'

export default {
  components : {
    TodoCard,
    TodoAddTaskForm,
    successToast,
    todoNavBar
  },
  setup () {

      const isAddingTodo = ref(false)
      const todosNb = ref (0)
      const state = reactive({todos : []})
      const stateTemp = reactive({todos : []})
      const healthCount = ref(0)
      const workCount = ref(0)
      const studiesCount = ref(0)
      const goalsCount = ref(0)
      const doneCount = ref(0)
    
      const handleAddingButtonEvent = () => {isAddingTodo.value=!isAddingTodo.value}

      // get todos number for each category
      const getTodoNumberCategory =  (category) => {
            let temp = ref([])
            if (category === 'Done')
            temp.value = state.todos.filter(todo => todo.isDone === true)
            else
            temp.value = state.todos.filter(todo => todo.category == category)
            return temp.value.length
      }

      // get Todos from database
      const getTodos = async () => {
        console.log('call to datatase ')
        fetch("http://localhost:3000/todos")
        .then(res => res.json())
        .then(data => {
          state.todos = data
          stateTemp.todos = data
          todosNb.value = data.length
          healthCount.value = getTodoNumberCategory('Health'),
          workCount.value = getTodoNumberCategory('Work'),
          studiesCount.value = getTodoNumberCategory('Studies'),
          goalsCount.value = getTodoNumberCategory('Goals')
          doneCount.value = getTodoNumberCategory('Done')
           
        })
        .catch (err => console.log(err))
      }

      //Add a new todo to database
      const addTodo = async (data) => {

       fetch("http://localhost:3000/todos", 
          {method: "POST",
              headers: {"Content-Type": "application/json",},
                  body: JSON.stringify(data),})
       .then(data => {
          if (data.status == 201)
          {
              getTodos()
              isAddingTodo.value=!isAddingTodo.value

          }
       })
       .catch (err => console.log(err))
  
      }

      //delete Todo from database

      const deleteTodo = async (id) => {

        fetch ("http://localhost:3000/todos/"+id,{method: 'DELETE',headers: {"Content-Type": "application/json"}})
        .then (data => {
          if (data.status == 200)
            {
              console.log("deleted succ")
              getTodos()
            }
        })
        .catch(err => console.log(err))
      }


      const checkTodo = (data) => {
        data.isDone = true

        fetch("http://localhost:3000/todos/"+data.id, 
          {method: "PUT",
              headers: {"Content-Type": "application/json",},
                  body: JSON.stringify(data),})
        .then (data => {
          if (data.status == 200)
          console.log("Success")
        }).catch (err => console.log(err))

      }


      //get All Todos before component mount
      onBeforeMount (() => {
        getTodos()
        
      })

      const handleGetTodosByCategory =  (category) => {

        stateTemp.todos=state.todos
        console.log(stateTemp.todos)
        if (category != 'All' && category != 'Done')
        stateTemp.todos = stateTemp.todos.filter(todo => todo.category === category)
        
        if(category === 'Done')
        {
          console.log(stateTemp.todos)
          stateTemp.todos = stateTemp.todos.filter(todo => todo.isDone)
        }
      }

      return {
        isAddingTodo,
        handleAddingButtonEvent,
        stateTemp,
        addTodo,
        successToast,
        deleteTodo,
        todosNb,
        workCount,
        healthCount,
        studiesCount,
        goalsCount,
        doneCount,
        handleGetTodosByCategory,
        checkTodo
      }
  }
}
</script>
