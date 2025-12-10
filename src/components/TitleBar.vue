<script setup></script>

<template>
  <div class="container">
    <section class="icon |">
      <img
        src="/images/illustration-working.svg"
        alt="An illustration of someone working on a computer" />
    </section>
    <section class="text |">
      <h1 class="">More than just shorter links</h1>
      <p class="">
        Build your brand’s recognition and get detailed insights on how your links are performing.
      </p>
      <button class="primary-btn">Get Started</button>
    </section>
  </div>
</template>

<style scoped>
.container {
  padding-inline: var(--spacing-500);
}

h1 {
  color: var(--gray-900);
  text-align: center;
  font-size: var(--fs-800);
  line-height: 110%;
}

.text p {
  text-align: center;
  margin-block: var(--spacing-150);
  max-width: 400px;
  margin-inline: auto;
}

.text button {
  margin-inline: auto;
  display: block;
  margin-bottom: var(--spacing-600);
}

.icon {
  margin-inline: auto;
  margin-block: var(--spacing-250);
}

.icon img {
  margin-inline: auto;
}

@media (min-width: 1024px) {
  .container {
    display: flex;
    gap: var(--spacing-200);
    align-items: start;
    padding-block: var(--spacing-500);
    justify-content: space-between;
  }

  .icon {
    order: 2;
    margin: 0;
  }

  .text {
    margin-top: var(--spacing-250);
  }

  h1 {
    text-align: start;
    margin-top: 0;
    max-width: 510px;
  }

  .text p {
    text-align: start;
    margin-inline: 0;
    max-width: 500px;
  }

  .text button {
    margin-inline: 0;
    margin-bottom: 0;
  }
}
</style>
