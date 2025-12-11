<script setup>
import { ref, watch } from 'vue'

const props = defineProps({
  urls: Array,
})

const emit = defineEmits(['remove-url'])
const copiedUrl = ref(null)
const shortUrls = ref({})

watch(() => props.urls, async (newUrls) => {
  for (const url of newUrls) {
    if (!shortUrls.value[url]) {
      shortUrls.value[url] = await shortenUrl(url)
    }
  }
}, { immediate: true, deep: true })

const copyToClipboard = async (url) => {
  try {
    await navigator.clipboard.writeText(shortUrls.value[url] || url)
    copiedUrl.value = url

    setTimeout(() => {
      emit('remove-url', url)
      copiedUrl.value = null
    }, 2000)
  } catch (err) {
    console.error('Failed to copy:', err)
  }
}

const shortenUrl = async (longUrl) => {
  try {
    const response = await fetch(`https://corsproxy.io/?${encodeURIComponent(`https://is.gd/create.php?format=simple&url=${encodeURIComponent(longUrl)}`)}`)
    const shortUrl = await response.text()
    
    if (shortUrl.includes('Error')) {
      console.error('Shortening failed:', shortUrl)
      return longUrl
    }
    
    return shortUrl.trim()
  } catch (err) {
    console.error('Error shortening URL:', err)
    return longUrl
  }
}
</script>

<template>
  <section class="container">
    <TransitionGroup name="fade" tag="div">
      <article class="clipboard" v-for="url in urls" :key="url">
        <p class="url">{{ url }}</p>
        <section class="shortened">
          <p>{{ shortUrls[url] || 'Shortening...' }}</p>
          <button
            class="primary-btn"
            :class="{ 'btn-active': copiedUrl === url }"
            @click="copyToClipboard(url)">
            {{ copiedUrl === url ? 'Copied!' : 'Copy' }}
          </button>
        </section>
      </article>
    </TransitionGroup>
  </section>
</template>

<style scoped>
.container {
  width: 100%;
}

.url {
  color: var(--gray-900);
  border-bottom: 1px solid var(--gray-400);
  padding-inline: var(--spacing-100);
  padding-block: var(--spacing-50);
}

.clipboard {
  width: 100%;
  border-radius: 12px;
  background-color: var(--white);
  margin-top: var(--spacing-150);
}

.shortened {
  padding-inline: var(--spacing-100);
  padding-block: var(--spacing-50);
}

.shortened p {
  color: var(--blue-400);
}

.shortened button {
  width: 100%;
  border-radius: 12px;
  margin-top: var(--spacing-100);
  font-weight: var(--weight-700);
}

.shortened .button-active {
  background-color: var(--purple-950);
}

.btn-active {
  background-color: var(--purple-950);
}

@media (min-width: 1024px) {
  .clipboard {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding-block: var(--spacing-100);
    padding-inline: var(--spacing-150);
  }
  .url {
    border-bottom: none;
    padding: 0;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    max-width: 500px;
    margin-right: var(--spacing-150);
  }
  .shortened {
    padding: 0;
    display: flex;
    align-items: center;
    gap: var(--spacing-150);
  }
  .shortened p {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    max-width: 300px;
  }
  .shortened button {
    margin-top: 0;
    width: 9rem;
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: all 0.3s ease;
}

.fade-enter-from {
  opacity: 0;
  transform: translateY(-10px);
}

.fade-leave-to {
  opacity: 0;
  transform: translateY(10px);
}

.fade-leave-active {
  position: absolute;
}
</style>
