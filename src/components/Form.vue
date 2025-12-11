<script setup>
import { ref } from 'vue'
import Clipboards from './Clipboards.vue'

const url = ref('')
const error = ref(false)
const errorMessage = ref('')
const urls = ref([])

const submitForm = () => {
  if (url.value.length <= 0) {
    error.value = true
    errorMessage.value = 'please provide a valid URL!'
  } else if (urls.value.includes(url.value)) {
    error.value = true
    errorMessage.value = 'This URL has already been added!'
  } else {
    error.value = false
    errorMessage.value = ''
    urls.value.push(url.value)
    url.value = ''
  }
}

const removeUrl = (urlToRemove) => {
  const index = urls.value.indexOf(urlToRemove)
  if (index > -1) {
    urls.value.splice(index, 1)
  }
}
</script>

<template>
  <div class="wrapper">
    <form @submit.prevent="submitForm">
      <input type="url" name="url" id="url" placeholder="Shorten a link here..." v-model="url" />
      <input type="submit" value="Shorten it!" />
      <p class="error" v-if="error">{{ errorMessage }}</p>
    </form>
    <div class="clipboard-wrapper">
      <Clipboards :urls="urls" @remove-url="removeUrl" />
    </div>
  </div>
</template>

<style scoped>
.wrapper {
  padding-inline: var(--spacing-500);
  position: relative;
  background-color: var(--purple-100);
}

form {
  background-color: var(--purple-950);
  background-image: url(/images/bg-shorten-mobile.svg);
  background-repeat: no-repeat;
  background-position: top right;
  border-radius: 12px;
  padding: var(--spacing-150);
  margin-bottom: -4rem;
  position: relative;
  top: -82px;
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
    top: -65px;
    margin-bottom: -3.5rem;
  }
  form input[type='submit'] {
    margin-top: 0;
    max-width: 20rem;
  }
  .error {
    bottom: 7px;
  }
}
</style>
