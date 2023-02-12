<script setup>

import TheAccordionItem from './TheAccordionItem.vue'
import faqs from '../data/faqs'

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
        />

    </dl>

</template>


<style scoped></style>