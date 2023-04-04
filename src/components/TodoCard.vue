<template>
<div :class="{'dark':isDark}">
<div :class="[s.container,{'rotate-1' :isGrabbed}]" 
        @mousedown="isGrabbed=true" 
            @mouseleave="isGrabbed=false"
                @mouseenter="isGrabbed=true">
    <div class="p-6">
    <div :class=s.title>
        <div class="flex justify-between items-center">
        <div>Sofware engineering</div>
        <div><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6 hover:text-cyan-700">
        <path stroke-linecap="round" stroke-linejoin="round" d="M11.25 4.5l7.5 7.5-7.5 7.5m-6-15l7.5 7.5-7.5 7.5" />
            </svg>
        </div>
        </div>
    </div>
    <p :class=s.p>
        Simple, flexible, get a clear view of who’s doing what and what needs to get done. 
    </p>
    </div>
</div>
</div>
</template>

<script>
import { ref } from 'vue'
import ArticleCardStyle from '@/tailwind/appStyles'

export default {
    props : ['task'],
    setup () {
       
        const isDark = ref(false)
        const isGrabbed = ref(false)
        const s = ref('')
        s.value = ArticleCardStyle.value
        return {
            isDark,
            s,
            isGrabbed
        }
    }
}
</script>