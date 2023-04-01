<template>
  <ArticleCard/>  
  <ArticleCard/>  
</template>

<script>
import ArticleCard from './components/ArticleCard.vue'
import ProfileCard from './components/ProfileCard.vue'

export default {
  components: { ArticleCard,ProfileCard },
  name: 'App',
}
</script>
