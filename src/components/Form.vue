<script setup>
import { ref } from 'vue'
const url = ref('')
const error = ref(false)
const clipboard = ref(false)
const shortenUrl = ref('')

const submitForm = () => {
  if (url.value.length <= 0) {
    error.value = true
  } else {
    error.value = false
    // SHORTEN THE URL THEN ADD IT TO USER'S CLIPBOPARD
    clipboard.value = true
    setTimeout(() => {
      clipboard.value = false
    }, 2000)
  }
}
</script>

<template>
  <div>
    <form @submit.prevent="submitForm">
      <input type="url" name="url" id="url" placeholder="Shorten a link here..." v-model="url" />
      <input type="submit" value="Shorten it!" />
      <p class="error" v-if="error">please provide a valid URL!</p>
      <Transition name="scale">
        <span class="clipboard" v-if="clipboard">
          <p>The URL : {{ shortenUrl }} has been copied to your clipboard!</p>
        </span>
      </Transition>
    </form>
  </div>
</template>

<style scoped>
div {
  padding-inline: var(--spacing-500);
  position: relative;
  background: linear-gradient(to bottom, var(--white) 50%, var(--purple-100) 50%);
}

form {
  background-color: var(--purple-950);
  background-image: url(/images/bg-shorten-mobile.svg);
  background-repeat: no-repeat;
  background-position: top right;
  border-radius: 12px;
  padding: var(--spacing-150);
  position: relative;
}

form > * {
  display: block;
  width: 100%;
}

form input[type='url'] {
  padding-block: 0.75rem;
  color: varr(var(--gray-500));
  padding-left: 0.5rem;
  border-radius: 4px;
  border: none;
}

form input[type='submit'] {
  border: none;
  margin-top: var(--spacing-100);
  background-color: var(--blue-400);
  border-radius: 4px;
  color: var(--white);
  padding-block: 0.75rem;
  cursor: pointer;
  transition: background-color 0.3s ease-in;
}

.error {
  position: absolute;
  bottom: 0;
  color: rgb(252, 114, 114);
  font-size: 1rem;
  width: 100%;
}

.clipboard {
  position: absolute;
  background-color: var(--white);
  inset: 1rem;
  border-radius: 12px;
  width: calc(100% - 2rem);
  display: grid;
  place-content: center;
  transition: 0.4s ease;
  transform-origin: center;
  display: block;
}

.clipboard p {
  color: var(--purple-600);
  font-size: var(--fs-450);
  text-align: center;
}

.scale-enter-active {
  animation: scaleIn 0.3s ease-out;
}

.scale-leave-active {
  animation: scaleOut 0.3s ease-in forwards;
}

@keyframes scaleIn {
  from {
    transform: scale(0);
    opacity: 0;
  }
  to {
    transform: scale(1);
    opacity: 1;
  }
}

@keyframes scaleOut {
  from {
    transform: scale(1);
    opacity: 1;
  }
  to {
    transform: scale(0);
    opacity: 0;
  }
}

@media (hover: hover) {
  form input[type='submit']:hover {
    background-color: var(--blue-400-o);
  }
}

@media (min-width: 1024px) {
  form {
    background-image: url(/images/bg-shorten-desktop.svg);
    background-repeat: no-repeat;
    background-position: center;
    background-size: cover;
    display: flex;
    align-items: center;
    gap: var(--spacing-200);
    padding-block: var(--spacing-250);
  }
  form input[type='submit'] {
    margin-top: 0;
    max-width: 20rem;
  }
}
</style>
