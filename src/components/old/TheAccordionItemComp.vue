<script setup>

// import ref
// NB we need onmounted because the ref will be null on first render
import { ref, onMounted, computed } from 'vue'

const ddEl = ref(null)

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

// temporary value for ddHeight bc ref to the dd element
// isn't available until it mounts
let ddHeight = '0px'
console.log(`ddHeight declared and is ${ddHeight}`)

// think this needs to be computed bc it depends on active
// it was proving tricky to do with a ternary expression in the template
const ddHeightComputed = computed(() => {
    console.log('ddHeight has been Computed')
    return props.active ? ddHeight : '0px'
})



onMounted(() => {

    // we don't have access to the ref ddEl
    // until mount, so ddHeight starts of with a temporary value
    // and is set to its proper value here

    ddHeight = `${ddEl.value.scrollHeight}px`
    console.log(`ddHeight updated by onMount and is ${ddHeight}`)
})

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
        :style="{ height: ddHeightComputed }"
    >
        <div :id="`accordion-dd-content-${itemIndex}`" class="accordion-desc">
            {{ answer }}
        </div>
    </dd>

</template>