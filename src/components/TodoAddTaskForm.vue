<template>
  <div class="bg-white dark:bg-slate-600 mt-2 mx-auto rounded-lg shadow-lg cursor-pointer border-3 p-6">
                <div>
                <label for="first_name" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Title</label>
                <input type="text" id="first_name" class="mb-3 bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Ex: shopping" required>
               </div>
               <div>
               <label for="message" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Description</label>
               <textarea id="message" rows="4" class="mb-3 block p-2.5 w-full text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Write your thoughts here..."></textarea>
               </div>
               <div>
                <button type="button" class="text-white w-full bg-blue-500 hover:bg-green-500 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-500">Save</button>
               </div>
            </div>
</template>

<script>
export default {

}
</script>

<style>

</style>