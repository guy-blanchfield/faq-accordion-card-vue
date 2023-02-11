<script setup>
// import HelloWorld from './components/HelloWorld.vue'
// import TheWelcome from './components/TheWelcome.vue'
import TheHeader from './components/TheHeader.vue'
import TheFooter from './components/TheFooter.vue'
import TheAccordion from './components/TheAccordion.vue'

// import the pictures
// NB not sure what the @ is doing, './assets' works as well - investigate
import illustrationWomanOnlineMobile from '@/assets/images/illustration-woman-online-mobile.svg'

</script>

<template>

  <TheHeader title="Frontend Mentor - FAQ Accordion Card - Vue"/>

  <main className="container">

    <section className="faq">

      <div className="faq-illustration">
  
        <picture>
          <source 
          :srcSet='illustrationWomanOnlineMobile'
          media="(min-width: 992px)" />
          <img :src='illustrationWomanOnlineMobile' alt="woman online" />
        </picture>

  </div>

  <div className="faq-faqs">

    <h2><abbr title="Frequently Asked Questions">FAQ</abbr></h2>

    <TheAccordion />

  </div>

</section>

</main>

  <TheFooter />

</template>

<style scoped>
/* probably don't need any scoped styles at the moment */
</style>
