<script setup>
import NavBar from './components/NavBar.vue'
import FooterBar from './components/FooterBar.vue'
import Banner from './components/Banner.vue'
import Stats from './components/Stats.vue'
import TitleBar from './components/TitleBar.vue'
import Form from './components/Form.vue'
</script>

<template>
  <header class="flex-al-center">
    <NavBar />
  </header>

  <main>
    <TitleBar />
    <Form />
    <Stats />
  </main>
  <Banner />
  <FooterBar />
</template>

<style scoped>
header {
  padding-inline: var(--spacing-500);
}

@media (min-width: 1024px) {
}
</style>
