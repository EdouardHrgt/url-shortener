<script setup>
import { ref } from 'vue'

const isOpen = ref(false)
</script>

<template>
  <div class="container | flex-al-center">
    <img src="/images/logo.svg" alt="Shortly" />
    <Transition name="burger-rotate" mode="out-in">
      <img
        v-if="!isOpen"
        key="burger"
        src="/images/burger-menu.png"
        alt="open navigation menu"
        class="burger"
        @click="isOpen = true" />
      <img
        v-else
        key="close"
        src="/images/close-icon.png"
        alt="close navigation menu"
        class="burger close"
        @click="isOpen = false" />
    </Transition>
    <div v-if="isOpen" class="overlay" @click="isOpen = false"></div>
    <nav class="flex-al-center" :class="{ 'nav-active': isOpen }">
      <ul class="navigation | flex-al-center">
        <li>Features</li>
        <li>Pricing</li>
        <li>Resources</li>
      </ul>
      <ul class="account | flex-al-center">
        <li>Login</li>
        <li data-signUp="true">Sign Up</li>
      </ul>
    </nav>
  </div>
</template>

<style scoped>
.container {
  justify-content: space-between;
  width: 100%;
  padding-block: var(--spacing-150);
  position: relative;
}

.burger {
  aspect-ratio: 1/1;
  width: 22px;
  cursor: pointer;
  opacity: 0.4;
  position: relative;
  z-index: 1001;
}

.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  background-color: rgba(12, 4, 24, 0.5);
  z-index: 999;
  touch-action: none;
}

nav {
  position: absolute;
  z-index: 1000;
  flex-direction: column;
  background-color: var(--purple-950);
  border-radius: 12px;
  width: 100%;
  top: 5.1rem;
  right: -250%;
  transition: right 0.3s ease-in;
  padding-block: var(--spacing-300);
  padding-inline: var(--spacing-200);
}

.nav-active {
  right: 0;
}

nav li {
  color: var(--white);
  font-weight: var(--weight-700);
  font-size: var(--fs-400);
  padding-block: var(--spacing-150);
  cursor: pointer;
  transition: color 0.3s ease-in;
}

nav ul {
  flex-direction: column;
  width: inherit;
  justify-content: center;
  align-items: center;
  padding-inline: 0;
}

nav .navigation {
  border-bottom: 1px solid var(--gray-400-o);
}

nav .account {
  padding: 0;
}

li[data-signUp='true'] {
  background-color: var(--blue-400);
  width: 100%;
  text-align: center;
  border-radius: 32px;
  padding-block: 0.8rem;
  transition: background-color 0.3s ease-in;
}

@media (hover: hover) {
  li:not([data-signUp]):hover {
    color: var(--gray-400);
  }
  li[data-signUp='true']:hover {
    background-color: var(--blue-400-o);
  }
}

@media (min-width: 900px) {
  .overlay {
    display: none;
  }
  
  nav {
    position: static;
    flex-direction: row;
    background-color: transparent;
    border-radius: 0;
    width: 100%;
    padding-block: 0;
    padding-inline: 0;
    margin-left: var(--spacing-300);
  }
  nav li {
    color: var(--gray-500);
    padding-block: 0;
  }
  nav ul {
    flex-direction: row;
    justify-content: flex-start;
    align-items: center;
  }
  nav .navigation {
    border-bottom: none;
  }
  .burger {
    display: none;
  }
  nav .navigation {
    gap: var(--spacing-200);
  }
  li[data-signUp='true'] {
    width: auto;
    padding-inline: var(--spacing-200);
    border-radius: 24px;
    color: var(--white);
  }
  nav .account {
    justify-content: flex-end;
    gap: var(--spacing-200);
  }
  @media (hover: hover) {
    li:not([data-signUp]):hover {
      color: var(--gray-900);
    }
  }
}

.burger-rotate-enter-active,
.burger-rotate-leave-active {
  transition: all 0.4s ease;
}

.burger-rotate-enter-from {
  transform: rotate(-90deg);
}

.burger-rotate-leave-to {
  transform: rotate(-90deg);
}

.burger-rotate-enter-to,
.burger-rotate-leave-from {
  transform: rotate(0deg);
}
</style>