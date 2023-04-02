<template>
  <div class="mx-auto">
    <div class="flex mt-6 p-3">
      <div id="todoSection" class="px-3 bg-slate-500 max-w-md rounded-md py-3">
        <div id="todoHead" class="flex justify-between py-1">
          <div class="text-white font-semibold">Todo</div>
          <div class="">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6 text-white cursor-pointer">
            <path stroke-linecap="round" stroke-linejoin="round" d="M6.75 12a.75.75 0 11-1.5 0 .75.75 0 011.5 0zM12.75 12a.75.75 0 11-1.5 0 .75.75 0 011.5 0zM18.75 12a.75.75 0 11-1.5 0 .75.75 0 011.5 0z" />
            </svg>
          </div>
        </div>
        <div v-if="isAddingTask" id="addToDoSection" class="py-2">
          <button v-if=isAddingTask class="bg-red-400 w-full p-2 rounded-md" @click='isAddingTask=false'>
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6 text-white font-black mx-auto">
              <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
          <button v-else class="bg-green-500 w-full p-2 rounded-md hover:bg-green-600" @click="isAddingTask=true">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6 text-white font-black mx-auto">
            <path stroke-linecap="round" stroke-linejoin="round" d="M12 4.5v15m7.5-7.5h-15" />
            </svg>
          </button>
          <div id="addingTaskForm">
          <div class="bg-white py-3 rounded-md max-w-md">

          </div>
        </div>
        </div>
        <div v-else id="todoBody">
          <article-card></article-card>
          <article-card></article-card>
        </div>
      </div>
      <div id="doing" class="px-3">
        <article-card></article-card>
      </div>
      <div id="done" class="px-3">
        <article-card></article-card>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'
import ArticleCard from './components/ArticleCard.vue'
import AddArticleButton from './components/AddArticleButton.vue'
import AddArticle from './components/AddArticle.vue'

export default {
  components: { ArticleCard, AddArticleButton, AddArticle },
  setup () {
    const isAddingTask = ref(true)
    return {
      isAddingTask
    }
  }
}
</script>
