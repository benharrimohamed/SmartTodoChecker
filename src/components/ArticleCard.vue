<template>
<div :class="{dark :isDark}">
<div :class="[style.container,{'rotate-3' :isGrabbed}]" 
        @mousedown="isGrabbed=true" 
            @mouseleave="isGrabbed=false"
                @mouseenter="isGrabbed=true">
    <div>
        <img src="https://avatars.githubusercontent.com/u/23489466?v=4" :class=style.image />
    </div>
    <div class="p-6">
    <div :class=style.title>
        Lorem ipsum dolor sit amet
    </div>
    <p :class=style.p>
        Lorem ipsum dolor, sit amet consectetur adipisicing elit.  vitae labore odit animi illum deserunt exercitationem dolores aut molestias ullam, consequatur ipsam commodi quam.
    </p>
    <div>
    <button @click="isDark=!isDark" :class=style.button>Change Theme</button>
    </div>
    </div>
</div>
</div>
</template>

<script>
import { ref } from 'vue'

export default {
    setup () {
        const isDark = ref(false)
        const isGrabbed = ref(false)
        const style = ref('')
        style.value = {
            
            title : 'text-slate-600 dark:text-white font-meduim text-lg mx-auto',
            p: 'text-slate-600 dark:text-white font-meduim mt-6 ',
            container: 'delay-150 sm:flex max-w-xl bg-white dark:bg-slate-600 mt-8 mx-auto rounded-lg shadow-lg',
            button : 'mx-auto text-white py-2 px-4 bg-slate-600 mt-6 rounded-full dark:bg-white dark:text-slate-600',
            image: 'md:h-full md:w-full md:object-cover md:rounded-l-lg h-28 w-28 sm:rounded-full mx-auto'
        }
        return {
            isDark,
            style,
            isGrabbed
        }
    }
}
</script>