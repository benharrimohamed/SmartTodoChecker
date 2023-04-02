<template>
  <div class="mx-auto max-w-md">
  <div :v-for="(task,id) in tasks">
    {{ task.id }}
  </div>
  <AddArticleButton/> 
  </div>
</template>

<script>
import { ref } from 'vue'
import AddArticleButton from './components/AddArticleButton.vue'
import ArticleCard from './components/ArticleCard.vue'

export default {
  setup () {

    const tasks = ref([])
    tasks.value = [
      {id: 1,title : 'title 1', desc: 'description'},
      {id: 2,title : 'title 2', desc: 'description'},
      {id: 3,title : 'title 3', desc: 'description'}
    ]

    return { ArticleCard, AddArticleButton , tasks}
  }
}
</script>
