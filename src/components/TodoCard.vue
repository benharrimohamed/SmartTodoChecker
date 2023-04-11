<template>
<div :class="{'rotate-1':isGrabbed}" 
@mouseleave="isGrabbed=false" 
@mouseenter="isGrabbed=true" class="bg-white dark:bg-slate-600 my-2 p-3 rounded-lg shadow-lg cursor-pointer ">
    <div class="text-slate-600 dark:text-white font-bold text-md mx-auto">
        <div class="flex justify-between items-center">
        <div>{{ todo.title }}</div>
        <div class="flex">
        <div v-if="!todo.isDone">
        <svg @click=handleTodoIsDone xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6 hover:text-green-500" alt="Mark as done">
        <path stroke-linecap="round" stroke-linejoin="round" d="M11.35 3.836c-.065.21-.1.433-.1.664 0 .414.336.75.75.75h4.5a.75.75 0 00.75-.75 2.25 2.25 0 00-.1-.664m-5.8 0A2.251 2.251 0 0113.5 2.25H15c1.012 0 1.867.668 2.15 1.586m-5.8 0c-.376.023-.75.05-1.124.08C9.095 4.01 8.25 4.973 8.25 6.108V8.25m8.9-4.414c.376.023.75.05 1.124.08 1.131.094 1.976 1.057 1.976 2.192V16.5A2.25 2.25 0 0118 18.75h-2.25m-7.5-10.5H4.875c-.621 0-1.125.504-1.125 1.125v11.25c0 .621.504 1.125 1.125 1.125h9.75c.621 0 1.125-.504 1.125-1.125V18.75m-7.5-10.5h6.375c.621 0 1.125.504 1.125 1.125v9.375m-8.25-3l1.5 1.5 3-3.75" />
        </svg>
        </div>
        <div v-else>
        <svg @click=handleUndoTodo xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6 hover:text-blue-500">
        <path stroke-linecap="round" stroke-linejoin="round" d="M15 15l-6 6m0 0l-6-6m6 6V9a6 6 0 0112 0v3" />
        </svg>
        </div>
        <svg @click=handleDeleteTodo xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" alt="Delete" stroke-width="1.5" stroke="currentColor" class="w-6 h-6 hover:text-red-500">
        <path stroke-linecap="round" stroke-linejoin="round" d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0" />
        </svg>
        </div>
        </div>
    </div>
    <p class="text-slate-600 dark:text-white font-meduim mt-3">
        {{todo.description}}
    </p>
</div>
</template>

<script>
import { reactive,ref } from 'vue'

export default {
    props: ["todo"],
    setup(props, {emit}) {
        const isGrabbed = ref(false)
        const todo = reactive(props.todo)
        const handleDeleteTodo = () => { emit ("deleteTodo",todo.id)}
        const handleTodoIsDone = () => { emit ("TodoIsDone",todo)}
        const handleUndoTodo = () => { emit ("undoTodo",todo)}

        return {
            todo,
            handleDeleteTodo,
            handleTodoIsDone,
            handleUndoTodo,
            isGrabbed
        }
    }
}
</script>