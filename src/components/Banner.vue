<script setup></script>

<template>
  <section>
    <h2 class="">Boost your links today</h2>
    <button class="primary-btn">Get Started</button>
  </section>
</template>

<style scoped>
section {
  background-color: var(--purple-950);
  width: 100%;
  text-align: center;
  padding-block: var(--spacing-300);
  background-image: url('/images/bg-boost-desktop.svg');
  background-repeat: no-repeat;
  background-size: cover;
}

h2 {
  color: var(--white);
  font-size: var(--fs-700);
  margin-bottom: var(--spacing-100);
}

@media (max-width: 900px) {
  section {
    background-image: url('/images/bg-boost-mobile.svg');
  }
}
</style>
