<script setup>

// import ref
import { ref } from 'vue'

const ddEl = ref(null)
// we don't have access to the ref ddEl
// until mount so optional chaining is used on the template ref
// see: :style="active ? { height: `${ddEl?.scrollHeight}px` }
// seems to work better than using computed and onmount
// in that it updates the value as soon as the ddEl is available
// How does it work? I don't know, but it does!

// declare the props
const props = defineProps({
    itemIndex: Number,
    faq: Object
})

// destructure the question and answer from faq
const { question, answer } = props.faq

// don't need emits in the multiple-panel-expansion

// do need some state here for whether or not this item is active
const active = ref(false)

const handleClick = () => {
    console.log(`clicky wicky and active being set to ${!active.value}`)
    active.value = !active.value
}


</script>

<template>

    <dt class="accordion-dt">
        <button
            @click="handleClick"
            type="button"
            :aria-expanded="active ? 'true' : 'false'"
            :aria-controls="`accordion-dd-content-${itemIndex}`"
        >
            {{ question }}
        </button>
    </dt>

    <dd 
        ref="ddEl" 
        class="accordion-dd" 
        :style="active ? { height: `${ddEl?.scrollHeight}px` } : 'height: 0px'"
    >
        <div :id="`accordion-dd-content-${itemIndex}`" class="accordion-desc">
            {{ answer }}
        </div>
    </dd>

</template>