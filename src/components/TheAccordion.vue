<script setup>

import TheAccordionItem from './TheAccordionItem.vue'
import faqs from '../data/faqs'

// import ref - you always forget this
import { ref } from 'vue'

// state for the index of the (i.e. expanded) item
const activeItem = ref(-1)

const handleClick = (n) => {
    // console.log(`Clickety wickety and n is ${n}`)
    // console.log(`activeItem.value: ${activeItem.value}`)
    if (activeItem.value === n) {
        return activeItem.value = -1
    }
    activeItem.value = n;
}

</script>


<template>

    <!-- makes sense to put the dl here -->
    <!-- with the dt and dd in TheAccordionItem that gets v-fored -->

    <dl class="accordion-dl">

    <!-- NB v-bind  for dynamic values or it treats everything as a string!!! -->
    <!-- (: is the shorthand e.g. :propname="propvalue") -->

        <TheAccordionItem
            v-for="(faq, index) in faqs" 
            :key="faq.question"
            :itemIndex="index"
            :faq="faq"
            :active="index === activeItem"
            @item-click="handleClick"
        />

    </dl>

</template>


<style scoped></style>