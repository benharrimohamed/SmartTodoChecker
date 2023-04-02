<template>
    <div>
      <input v-model=title type="text" placeholder="Title" class="mt-6 block w-full rounded-md border-0 py-1.5 pl-3 pr-20 text-green-800 ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-green-800 sm:text-sm sm:leading-6"/>
      <textarea v-model=description placeholder="Description" class="mt-2 block w-full rounded-md border-0 py-1.5 pl-3 pr-20 text-green-800 ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-green-800 sm:text-sm sm:leading-6">
      </textarea>
      <add-article-button @click="handleAddArticle"/>
    </div>
  </template>
  
  <script>
  import AddArticleButton from './AddArticleButton.vue';
  export default {
    components : {AddArticleButton},
    setup (context) {
        const title = ref('')
        const description = ref('')
       
        
        return {
            title,description
        }
    }
  
  }
  </script>
  
  <style>
  
  </style>