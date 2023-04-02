<template>
<div :class="{'dark':isDark}">
<div :class="[s.container,{'rotate-3' :isGrabbed}]" 
        @mousedown="isGrabbed=true" 
            @mouseleave="isGrabbed=false"
                @mouseenter="isGrabbed=true">
    <div class="p-6">
    <div :class=s.title>
        Finding a job
    </div>
    <p :class=s.p>
        Lorem ipsum dolor, sit amet consectetur adipisicing elit. aut molestias ullam, consequatur ipsam commodi quam.
    </p>
    </div>
</div>
</div>
</template>

<script>
import { ref, toRef } from 'vue'
import ArticleCardStyle from '@/tailwind/appStyles'

export default {
    setup (props) {
        const isDark = ref(false)
        const isGrabbed = ref(false)
        const s = ref('')
        const {task} = toRef(props)
        console.log(task.value)
        s.value = ArticleCardStyle.value
        console.log(ArticleCardStyle.value)
        return {
            isDark,
            s,
            isGrabbed
        }
    }
}
</script>