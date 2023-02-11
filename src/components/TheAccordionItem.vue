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
    faq: Object,
    active: Boolean
})

// destructure the question and answer from faq
const { question, answer } = props.faq

// declare the emits that we're going to use
const emit = defineEmits(['itemClick'])


</script>

<template>

    <dt class="accordion-dt">
        <button
            @click="$emit('itemClick', itemIndex)"
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