<template>
  <div :class="{ dark: darkMode }" class="w-full p-4 border border-red-300">
    <div
      class="w-full p-2 h-screen rounded-md shadow-md bg-blue-500 dark:bg-gray-500 md:w-1/2 md:mx-auto overflow-y-auto"
    >
      <div class="flex justify-between">
        <div class="text-white font-bold">Todos</div>

        <button @click="darkMode = !darkMode">
          <svg
            v-if="!darkMode"
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="w-6 h-6 text-white"
            fill="white"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M21.752 15.002A9.718 9.718 0 0118 15.75c-5.385 0-9.75-4.365-9.75-9.75 0-1.33.266-2.597.748-3.752A9.753 9.753 0 003 11.25C3 16.635 7.365 21 12.75 21a9.753 9.753 0 009.002-5.998z"
            />
          </svg>
          <svg
            v-else
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="w-6 h-6 text-white"
            fill="white"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M12 3v2.25m6.364.386l-1.591 1.591M21 12h-2.25m-.386 6.364l-1.591-1.591M12 18.75V21m-4.773-4.227l-1.591 1.591M5.25 12H3m4.227-4.773L5.636 5.636M15.75 12a3.75 3.75 0 11-7.5 0 3.75 3.75 0 017.5 0z"
            />
          </svg>
        </button>
      </div>
      <div>
        <button
          class="bg-white py-1 w-full rounded-md mt-2 dark:bg-gray-400"
          @click="handleAddingButtonEvent"
        >
          <svg
            v-if="isAddingTodo"
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="w-6 h-6 mx-auto dark:text-white text-red-500"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M6 18L18 6M6 6l12 12"
            />
          </svg>

          <svg
            v-else
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="w-6 h-6 mx-auto dark:text-white text-blue-500"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M12 4.5v15m7.5-7.5h-15"
            />
          </svg>
        </button>
      </div>
      <todoNavBar
        v-if="!isAddingTodo"
        :doneCount="doneCount"
        :healthCount="healthCount"
        :workCount="workCount"
        :studiesCount="studiesCount"
        :goalsCount="goalsCount"
        @getTodosBy="handleGetTodosByCategory"
        :todosNb="todosNb"
      ></todoNavBar>
      <TodoAddTaskForm
        v-if="isAddingTodo"
        @addNewTodo="addTodo"
      ></TodoAddTaskForm>
      <div v-else-if="stateTemp.todos.length > 0">
        <div class="border border-red-300 h-screen overflow-y-auto mb-3">
          <div v-for="todo in stateTemp.todos" :key="todo.id">
            <TodoCard
              :todo="todo"
              @TodoIsDone="checkTodo"
              @deleteTodo="deleteTodo"
              @undoTodo="undoTodo"
            ></TodoCard>
          </div>
        </div>
      </div>
      <div v-else class="py-2 bg-blue-300 mt-2 rounded-md dark:bg-gray-400">
        <div class="mx-auto text-blue-600 font-meduim w-fit dark:text-gray-700">
          Nothing here !
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import TodoCard from "./components/TodoCard.vue";
import { onBeforeMount, reactive, ref, computed } from "vue";
import TodoNavBar from "./components/TodoNavBar.vue";
import SearchTodo from "./components/SearchTodo.vue";
import TodoAddTaskForm from "./components/TodoAddTaskForm.vue";

export default {
  components: {
    TodoCard,
    TodoNavBar,
    SearchTodo,
    TodoAddTaskForm,
  },
  setup() {
    const darkMode = ref(false);
    const isAddingTodo = ref(false);
    const todosNb = ref(0);
    const state = reactive({ todos: [] });
    const stateTemp = reactive({ todos: [] });
    const healthCount = ref(0);
    const workCount = ref(0);
    const studiesCount = ref(0);
    const goalsCount = ref(0);
    const doneCount = ref(0);
    const searchInput = ref("");
    const apiURL = new URL("http://localhost:3000/todos");

    // Show and hide the add Todo form
    const handleAddingButtonEvent = () => {
      isAddingTodo.value = !isAddingTodo.value;
    };

    // Count todos for each category
    const getTodoNumberCategory = (category) => {
      let temp = ref([]);
      if (category === "Done")
        temp.value = state.todos.filter((todo) => todo.isDone === true);
      else temp.value = state.todos.filter((todo) => todo.category == category);
      return temp.value.length;
    };

    // Get All Todos from database
    const getTodos = async () => {
      fetch(apiURL) //Fetch data from the Api url (GET)
        .then((res) => res.json())
        .then((data) => {
          state.todos = data;
          state.todos.sort((t1, t2) => Number(t2.isDone) - Number(t1.isDone)); // sort Todos by completion state
          stateTemp.todos = data; // assigned data to a temporory array
          todosNb.value = data.length; // get total number of todos

          (healthCount.value = getTodoNumberCategory("Health")), // get number of Todos by Health
            (workCount.value = getTodoNumberCategory("Work")), // get number of Todos by Work
            (studiesCount.value = getTodoNumberCategory("Studies")), // get number of Todos by Studies
            (goalsCount.value = getTodoNumberCategory("Goals")); // get number of Todos by Goals
          doneCount.value = getTodoNumberCategory("Done"); // get number of completed Todos
        })
        .catch((err) => console.log(err)); //In case of error Console lof the error
    };

    //Add a new todo to database
    const addTodo = async (data) => {
      fetch(apiURL, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(data),
      })
        .then((data) => {
          if (data.status == 201) {
            getTodos();
            isAddingTodo.value = !isAddingTodo.value;
          }
        })
        .catch((err) => console.log(err));
    };

    //delete Todo from database

    const deleteTodo = async (id) => {
      fetch(apiURL + id, {
        method: "DELETE",
        headers: { "Content-Type": "application/json" },
      })
        .then((data) => {
          if (data.status == 200) {
            console.log("deleted succ");
            getTodos();
          }
        })
        .catch((err) => console.log(err));
    };

    const checkTodo = (todo) => {
      todo.isDone = true;

      fetch(apiURL + todo.id, {
        method: "PUT",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(todo),
      })
        .then((data) => {
          if (data.status == 200) getTodos();
        })
        .catch((err) => console.log(err));
    };

    const undoTodo = (todo) => {
      todo.isDone = false;
      fetch(apiURL + todo.id, {
        method: "PUT",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(todo),
      })
        .then((data) => {
          if (data.status == 200) getTodos();
        })
        .catch((err) => console.log(err));
    };

    //get All Todos before component mount
    onBeforeMount(() => {
      getTodos();
    });

    const handleGetTodosByCategory = (category) => {
      stateTemp.todos = state.todos;
      console.log(stateTemp.todos);
      if (category != "All" && category != "Done")
        stateTemp.todos = stateTemp.todos.filter(
          (todo) => todo.category === category
        );

      if (category === "Done") {
        console.log(stateTemp.todos);
        stateTemp.todos = stateTemp.todos.filter((todo) => todo.isDone);
      }
    };

    const lookUpForTodo = (input) => {
      console.log(input);
    };

    return {
      isAddingTodo,
      handleAddingButtonEvent,
      stateTemp,
      addTodo,
      deleteTodo,
      todosNb,
      workCount,
      healthCount,
      studiesCount,
      goalsCount,
      doneCount,
      handleGetTodosByCategory,
      checkTodo,
      undoTodo,
      darkMode,
      searchInput,
      lookUpForTodo,
    };
  },
};
</script>
