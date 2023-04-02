<template>
<div :class="{'dark':isDark}">
<div :class="[s.container,{'rotate-3' :isGrabbed}]" 
        @mousedown="isGrabbed=true" 
            @mouseleave="isGrabbed=false"
                @mouseenter="isGrabbed=true">
    <div class="p-6">
    <div :class=s.title>
        Sofware engineering
    </div>
    <p :class=s.p>
        Simple, flexible, get a clear view of who’s doing what and what needs to get done. Learn more in our guide for getting started. and powerful. All it takes are boards, lists, and cards to get a clear view of who’s doing what and what needs to get done. Learn more in our guide for getting started.
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