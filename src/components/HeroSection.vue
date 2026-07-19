<template>
  <section class="hero" id="hero">
    <div class="hero__overlay"></div>
    <div class="hero__vignette"></div>

    <!-- Decorative top border -->
    <div class="hero__top-decor">
      <span class="hero__decor-line"></span>
    </div>

    <div class="hero__content">
      <p class="hero__families" :class="{ 'hero__animate': animate }" style="--delay: 0.2s">
        Together with their families
      </p>

      <h1 class="hero__names" :class="{ 'hero__animate': animate }" style="--delay: 0.6s">
        Omar <span class="hero__amp">&</span> Mariyem
      </h1>

      <div class="hero__ornament" :class="{ 'hero__animate': animate }" style="--delay: 1s">
        <span class="hero__orn-line"></span>
        <span class="hero__orn-diamond">◆</span>
        <span class="hero__orn-line"></span>
      </div>

      <p class="hero__date" :class="{ 'hero__animate': animate }" style="--delay: 1.2s">
        30 &nbsp;|&nbsp; 07 &nbsp;|&nbsp; 2026
      </p>

      <p class="hero__venue-hint" :class="{ 'hero__animate': animate }" style="--delay: 1.5s">
        Request the honour of your presence at our engagement
      </p>
    </div>

    <div class="hero__scroll-hint" :class="{ 'hero__animate': animate }" style="--delay: 2s">
      <span>Scroll Down</span>
      <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <polyline points="6 9 12 15 18 9"></polyline>
      </svg>
    </div>

    <!-- Decorative bottom fade -->
    <div class="hero__bottom-fade"></div>
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
    rgba(246, 238, 242, 0.4) 0%,
    rgba(255, 251, 247, 0.3) 30%,
    rgba(137, 120, 158, 0.2) 50%,
    rgba(255, 251, 247, 0.4) 70%,
    rgba(251, 248, 252, 0.8) 100%
  );
}

.hero__vignette {
  position: absolute;
  inset: 0;
  background: radial-gradient(ellipse at center, transparent 40%, rgba(75, 61, 91, 0.2) 100%);
}

.hero__top-decor {
  position: absolute;
  top: 2rem;
  left: 50%;
  transform: translateX(-50%);
  z-index: 2;
}

.hero__decor-line {
  display: block;
  width: 40px;
  height: 1px;
  background: var(--color-gold);
  opacity: 0.4;
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
  font-size: 0.6rem;
  font-weight: 400;
  letter-spacing: 0.4em;
  text-transform: uppercase;
  color: var(--color-navy-light);
  opacity: 0;
  transform: translateY(20px);
  margin-bottom: 1.75rem;
}

/* Couple names */
.hero__names {
  font-family: var(--font-cursive);
  font-size: 3.8rem;
  color: var(--color-navy);
  line-height: 1.15;
  text-shadow: 0 4px 20px rgba(75, 61, 91, 0.1);
  opacity: 0;
  transform: translateY(20px);
}

.hero__amp {
  display: inline-block;
  font-size: 2.8rem;
  color: var(--color-gold-light);
  margin: 0 0.15rem;
  text-shadow: 0 2px 10px rgba(201, 169, 110, 0.15);
}

/* Ornamental divider */
.hero__ornament {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  margin: 1.5rem auto;
  opacity: 0;
  transform: translateY(20px);
}

.hero__orn-line {
  width: 40px;
  height: 1px;
  background: linear-gradient(90deg, transparent, var(--color-gold), transparent);
}

.hero__orn-diamond {
  font-size: 0.4rem;
  color: var(--color-gold);
}

/* Date */
.hero__date {
  font-family: var(--font-serif);
  font-size: 1.15rem;
  font-weight: 400;
  letter-spacing: 0.25em;
  color: var(--color-navy);
  opacity: 0;
  transform: translateY(20px);
  text-shadow: 0 2px 10px rgba(75, 61, 91, 0.05);
}

/* Venue hint */
.hero__venue-hint {
  font-family: var(--font-sans);
  font-size: 0.62rem;
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
  bottom: 2.5rem;
  left: 50%;
  transform: translateX(-50%);
  z-index: 2;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.35rem;
  color: var(--color-navy-light);
  opacity: 0;
}

.hero__scroll-hint span {
  font-family: var(--font-sans);
  font-size: 0.55rem;
  letter-spacing: 0.25em;
  text-transform: uppercase;
}

.hero__scroll-hint svg {
  animation: bounceSoft 2s infinite;
}

/* Bottom fade */
.hero__bottom-fade {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 100px;
  background: linear-gradient(to bottom, transparent, var(--color-warm-gray));
  z-index: 1;
}

/* Animation trigger class */
.hero__animate {
  animation: fadeInUp 0.8s ease forwards;
  animation-delay: var(--delay, 0s);
}
</style>
