<template>
    <div class="grid grid-rows-3 m-3 p-4 border border-red-300">
      <div class="mx-auto w-full border-red-300 p-2 rounded-md shadow-md bg-slate-400 md:mw-1/3 border">
        <div class="flex justify-between">
         <div class="text-white font-bold">Todos</div>
         <div>
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6 text-white">
           <path stroke-linecap="round" stroke-linejoin="round" d="M6.75 12a.75.75 0 11-1.5 0 .75.75 0 011.5 0zM12.75 12a.75.75 0 11-1.5 0 .75.75 0 011.5 0zM18.75 12a.75.75 0 11-1.5 0 .75.75 0 011.5 0z" />
          </svg>
        </div>
       </div>
       <TodoCard></TodoCard>
       <TodoCard></TodoCard>
       
     </div>
   </div>
</template>

<script>
import TodoCard from './components/TodoCard.vue';
export default {
  components : {
    TodoCard
  }
}
</script>
