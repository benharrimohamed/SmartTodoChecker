<template>
  <form @submit.prevent="handleAddNewTodo">
  <div class="bg-white dark:bg-slate-600 mt-2 mx-auto rounded-lg shadow-lg cursor-pointer border-3 p-6">
                <div>
                <label for="first_name" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Title</label>
                <input v-model=newTodo.title type="text" id="first_name" class="mb-3 bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Ex: shopping" required>
               </div>
               <div>
               <label for="message" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Description</label>
               <textarea v-model=newTodo.description id="message" rows="4" class="mb-3 block p-2.5 w-full text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Write your thoughts here..."></textarea>
               </div>
               <div>
                <label for="small" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Category</label>
                 <select v-model="newTodo.category" id="small" class="block w-full p-2 mb-6 text-sm text-gray-900 border border-gray-300 rounded-lg bg-gray-50 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
                  <option selected value="Work"  class="text-yellow-500 font-meduim">Work</option>
                  <option value="Health" class="text-green-500 font-meduim">Health</option>
                  <option value="Studies" class="text-blue-500 font-meduim">Studies</option>
                  <option value="Goals" class="text-purple-500 font-meduim">Daily Goals</option>
                </select>
               </div>
               <div>
                <button type="submit" class="text-white w-full bg-blue-500 hover:bg-green-500 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-500">Save</button>
               </div>
            </div>
  </form>
</template>

<script>
import { reactive } from 'vue'
export default {

  setup(props, {emit}) {


    const newTodo = reactive(
      {
        title:'', 
        description:'',
        category : ''
      })

    

    const handleAddNewTodo = () => {
      emit("addNewTodo",newTodo)
    }

    return {
      newTodo,
      handleAddNewTodo
    }
  }

}
</script>

<style>

</style>