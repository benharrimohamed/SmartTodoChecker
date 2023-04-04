<template>
  <div id="addToDoSection" class="py-2">
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
        </div>
</template>

<script>
export default {

}
</script>

<style>

</style>