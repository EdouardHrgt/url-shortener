<script setup>
import NavBar from './components/NavBar.vue'
import FooterBar from './components/FooterBar.vue'
</script>

<template>
  <header class="flex-al-center">
    <NavBar />
  </header>

  <main></main>

  <FooterBar />
</template>

<style scoped>
header,
main {
  padding-inline: var(--spacing-500);
}

@media (min-width: 1024px) {
}
</style>
