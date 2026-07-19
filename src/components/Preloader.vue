<template>
  <transition name="preloader-fade">
    <div v-if="visible" class="preloader">
      <div class="preloader__content">
        <div class="preloader__initials">
          <span class="preloader__letter">O</span>
          <span class="preloader__ampersand">&</span>
          <span class="preloader__letter">M</span>
        </div>
        <div class="preloader__line"></div>
        <p class="preloader__tagline">We invite you to celebrate</p>
      </div>
    </div>
  </transition>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const emit = defineEmits(['loaded'])
const visible = ref(true)

onMounted(() => {
  const minDelay = new Promise(resolve => setTimeout(resolve, 2800))
  const assetsReady = new Promise(resolve => {
    if (document.readyState === 'complete') {
      resolve()
    } else {
      window.addEventListener('load', resolve, { once: true })
    }
  })

  Promise.all([minDelay, assetsReady]).then(() => {
    visible.value = false
    setTimeout(() => emit('loaded'), 600)
  })
})
</script>

<style scoped>
.preloader {
  position: fixed;
  inset: 0;
  z-index: 9999;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, var(--color-navy-dark), var(--color-navy), var(--color-navy-light));
}

.preloader__content {
  text-align: center;
  animation: pulseSoft 2s ease-in-out infinite;
}

.preloader__initials {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.75rem;
}

.preloader__letter {
  font-family: var(--font-serif);
  font-size: 4rem;
  font-weight: 600;
  color: var(--color-ivory);
  letter-spacing: 0.05em;
}

.preloader__ampersand {
  font-family: var(--font-cursive);
  font-size: 3.5rem;
  color: var(--color-gold);
}

.preloader__line {
  width: 60px;
  height: 1px;
  background: var(--color-gold);
  margin: 1.25rem auto;
  animation: shimmer 2s linear infinite;
  background: linear-gradient(90deg, transparent, var(--color-gold), transparent);
  background-size: 200% 100%;
}

.preloader__tagline {
  font-family: var(--font-sans);
  font-size: 0.75rem;
  letter-spacing: 0.3em;
  text-transform: uppercase;
  color: var(--color-gold-light);
  opacity: 0.8;
}

/* Transition */
.preloader-fade-leave-active {
  transition: opacity 0.6s ease;
}
.preloader-fade-leave-to {
  opacity: 0;
}
</style>
