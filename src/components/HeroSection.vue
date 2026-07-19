<template>
  <section class="hero" id="hero">
    <div class="hero__overlay"></div>
    <div class="hero__content">
      <p class="hero__families" :class="{ 'hero__animate': animate }" style="--delay: 0.2s">
        Together with their families
      </p>

      <h1 class="hero__names" :class="{ 'hero__animate': animate }" style="--delay: 0.6s">
        Omar <span class="hero__amp">&</span> Mariyem
      </h1>

      <div class="hero__divider" :class="{ 'hero__animate': animate }" style="--delay: 1s"></div>

      <p class="hero__date" :class="{ 'hero__animate': animate }" style="--delay: 1.2s">
        30 &nbsp;|&nbsp; 07 &nbsp;|&nbsp; 2026
      </p>

      <p class="hero__venue-hint" :class="{ 'hero__animate': animate }" style="--delay: 1.5s">
        Request the honour of your presence at our engagement
      </p>
    </div>

    <div class="hero__scroll-hint" :class="{ 'hero__animate': animate }" style="--delay: 2s">
      <span>Scroll Down</span>
      <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <polyline points="6 9 12 15 18 9"></polyline>
      </svg>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import heroBg from '@/assets/images/hero-bg.png'

const animate = ref(false)

onMounted(() => {
  setTimeout(() => {
    animate.value = true
  }, 300)
})
</script>

<style scoped>
.hero {
  position: relative;
  min-height: 100vh;
  min-height: 100dvh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-image: v-bind("`url('${heroBg}')`");
  background-size: cover;
  background-position: center;
  overflow: hidden;
}

.hero__overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(
    to bottom,
    rgba(26, 39, 68, 0.55) 0%,
    rgba(26, 39, 68, 0.40) 40%,
    rgba(26, 39, 68, 0.60) 100%
  );
}

.hero__content {
  position: relative;
  z-index: 2;
  text-align: center;
  padding: 2rem 1.5rem;
}

/* Families text */
.hero__families {
  font-family: var(--font-sans);
  font-size: 0.65rem;
  font-weight: 400;
  letter-spacing: 0.35em;
  text-transform: uppercase;
  color: var(--color-ivory);
  opacity: 0;
  transform: translateY(20px);
  margin-bottom: 1.5rem;
}

/* Couple names */
.hero__names {
  font-family: var(--font-cursive);
  font-size: 3.5rem;
  color: #fff;
  line-height: 1.15;
  text-shadow: 0 2px 20px rgba(0, 0, 0, 0.3);
  opacity: 0;
  transform: translateY(20px);
}

.hero__amp {
  display: inline-block;
  font-size: 2.5rem;
  color: var(--color-gold-light);
  margin: 0 0.25rem;
}

/* Divider */
.hero__divider {
  width: 60px;
  height: 1px;
  background: var(--color-gold);
  margin: 1.5rem auto;
  opacity: 0;
  transform: translateY(20px);
}

/* Date */
.hero__date {
  font-family: var(--font-serif);
  font-size: 1.1rem;
  font-weight: 400;
  letter-spacing: 0.2em;
  color: var(--color-ivory);
  opacity: 0;
  transform: translateY(20px);
}

/* Venue hint */
.hero__venue-hint {
  font-family: var(--font-sans);
  font-size: 0.7rem;
  font-weight: 300;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--color-gold-light);
  margin-top: 1.5rem;
  opacity: 0;
  transform: translateY(20px);
}

/* Scroll hint */
.hero__scroll-hint {
  position: absolute;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%);
  z-index: 2;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.25rem;
  color: var(--color-ivory);
  opacity: 0;
}

.hero__scroll-hint span {
  font-family: var(--font-sans);
  font-size: 0.6rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
}

.hero__scroll-hint svg {
  animation: bounceSoft 2s infinite;
}

/* Animation trigger class */
.hero__animate {
  animation: fadeInUp 0.8s ease forwards;
  animation-delay: var(--delay, 0s);
}
</style>
