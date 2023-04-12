<template>
  <div class="overflow-x-auto flex mt-2 space-x-4 items-center">
    <div
      @click="handleAllTodos"
      class="dark:bg-gray-400 border border-white flex justify-between items-center cursor-pointer bg-cyan-500 px-2 py-1 text-white rounded-full shadow-lg"
    >
      All
      <span
        class="dark:bg-gray-600 dark:text-white ml-2 inline-flex items-center justify-center w-4 h-4 text-xs font-semibold text-cyan-800 bg-cyan-200 rounded-full"
        >{{ todosNb }}</span
      >
    </div>
    <div
      @click="handleDoneTodos"
      class="dark:bg-gray-400 border border-white flex justify-between items-center cursor-pointer bg-red-500 px-2 py-1 text-white rounded-full shadow-lg"
    >
      Done
      <span
        class="dark:bg-gray-600 dark:text-white ml-1 inline-flex items-center justify-center w-4 h-4 text-xs font-semibold text-red-800 bg-red-200 rounded-full"
        >{{ doneCount }}</span
      >
    </div>
    <div
      @click="handleHealthTodos"
      class="dark:bg-gray-400 border border-white flex justify-between items-center cursor-pointer bg-yellow-500 px-2 py-1 text-white rounded-full shadow-lg"
    >
      Health
      <span
        class="dark:bg-gray-600 dark:text-white ml-1 inline-flex items-center justify-center w-4 h-4 text-xs font-semibold text-yellow-800 bg-yellow-200 rounded-full"
        >{{ healthCount }}</span
      >
    </div>
    <div
      @click="handleWorkTodos"
      class="dark:bg-gray-400 border border-white flex justify-between items-center cursor-pointer bg-green-500 px-2 py-1 text-white rounded-full shadow-lg"
    >
      Work
      <span
        class="dark:bg-gray-600 dark:text-white ml-1 inline-flex items-center justify-center w-4 h-4 text-xs font-semibold text-green-800 bg-green-200 rounded-full"
        >{{ workCount }}</span
      >
    </div>
    <div
      @click="handleStudieTodos"
      class="dark:bg-gray-400 border border-white flex justify-between items-center cursor-pointer bg-purple-500 px-2 py-1 text-white rounded-full shadow-lg"
    >
      Studies
      <span
        class="dark:bg-gray-600 dark:text-white ml-1 inline-flex items-center justify-center w-4 h-4 text-xs font-semibold text-purple-800 bg-purple-200 rounded-full"
        >{{ studiesCount }}</span
      >
    </div>
    <div
      @click="handleGoalTodos"
      class="dark:bg-gray-400 border border-white flex justify-between items-center cursor-pointer bg-gray-500 px-2 py-1 text-white rounded-full shadow-lg"
    >
      Goals
      <span
        class="dark:bg-gray-600 dark:text-white ml-1 inline-flex items-center justify-center w-4 h-4 text-xs font-semibold text-gray-800 bg-gray-200 rounded-full"
        >{{ goalsCount }}</span
      >
    </div>
  </div>
</template>

<script>
export default {
  props: [
    "healthCount",
    "workCount",
    "studiesCount",
    "goalsCount",
    "todosNb",
    "doneCount",
  ],
  setup(props, { emit }) {
    const handleAllTodos = () => {
      emit("getTodosBy", "All");
    };
    const handleDoneTodos = () => {
      emit("getTodosBy", "Done");
    };
    const handleHealthTodos = () => {
      emit("getTodosBy", "Health");
    };
    const handleWorkTodos = () => {
      emit("getTodosBy", "Work");
    };
    const handleStudieTodos = () => {
      emit("getTodosBy", "Studies");
    };
    const handleGoalTodos = () => {
      emit("getTodosBy", "Goals");
    };

    return {
      handleGoalTodos,
      handleAllTodos,
      handleHealthTodos,
      handleStudieTodos,
      handleWorkTodos,
      handleDoneTodos,
    };
  },
};
</script>
