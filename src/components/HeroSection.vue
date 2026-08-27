<template>
  <section class="hero" id="hero">
    <!-- Top & bottom soft lighting gradients -->
    <div class="hero__overlay-top"></div>
    <div class="hero__overlay-bottom"></div>

    <!-- Top header & names: positioned in the open canvas above the portrait -->
    <div class="hero__header">
      <div class="hero__top-decor" :class="{ 'hero__animate': animate }" style="--delay: 0.1s">
        <span class="hero__decor-line"></span>
        <span class="hero__decor-diamond">✦</span>
        <span class="hero__decor-line"></span>
      </div>

      <p class="hero__families" :class="{ 'hero__animate': animate }" style="--delay: 0.25s">
        Together with their families
      </p>

      <div class="hero__names-wrap" :class="{ 'hero__animate': animate }" style="--delay: 0.45s">
        <h1 class="hero__names">
          Mahmoud <span class="hero__amp">&</span> Radwa
        </h1>
      </div>

      <div class="hero__ornament" :class="{ 'hero__animate': animate }" style="--delay: 0.65s">
        <span class="hero__orn-line"></span>
        <span class="hero__orn-diamond">◆</span>
        <span class="hero__orn-line"></span>
      </div>

      <p class="hero__date" :class="{ 'hero__animate': animate }" style="--delay: 0.85s">
        09 &nbsp;|&nbsp; 09 &nbsp;|&nbsp; 2026
      </p>
    </div>

    <!-- Bottom content: placed cleanly at footer without obstructing the children -->
    <div class="hero__footer">
      <div class="hero__badge-wrap" :class="{ 'hero__animate': animate }" style="--delay: 1.05s">
        <p class="hero__venue-hint">
          Request the honour of your presence at our wedding
        </p>
      </div>

      <div class="hero__scroll-hint" :class="{ 'hero__animate': animate }" style="--delay: 1.25s">
        <span>Scroll Down</span>
        <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <polyline points="6 9 12 15 18 9"></polyline>
        </svg>
      </div>
    </div>

    <!-- Decorative bottom fade connecting to next section -->
    <div class="hero__bottom-fade"></div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import heroBg from '@/assets/images/two_person.png'

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
  justify-content: space-between;
  align-items: center;
  background-image: v-bind("`url('${heroBg}')`");
  background-size: cover;
  background-position: center bottom;
  overflow: hidden;
  padding: 3rem 1.5rem 1.75rem;
}

/* Subtle top gradient for luminous contrast on names */
.hero__overlay-top {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 40%;
  background: linear-gradient(
    to bottom,
    rgba(250, 246, 240, 0.85) 0%,
    rgba(250, 246, 240, 0.45) 55%,
    transparent 100%
  );
  pointer-events: none;
  z-index: 1;
}

/* Very subtle bottom vignette */
.hero__overlay-bottom {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 25%;
  background: linear-gradient(
    to top,
    rgba(250, 246, 240, 0.8) 0%,
    rgba(250, 246, 240, 0.3) 60%,
    transparent 100%
  );
  pointer-events: none;
  z-index: 1;
}

/* ── Top Header & Names ── */
.hero__header {
  position: relative;
  z-index: 2;
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
  max-width: 380px;
  margin-top: 0.25rem;
}

.hero__top-decor {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.4rem;
  opacity: 0;
  transform: translateY(-10px);
}

.hero__decor-line {
  display: block;
  width: 32px;
  height: 1px;
  background: linear-gradient(90deg, transparent, var(--color-gold-dark), transparent);
}

.hero__decor-diamond {
  font-size: 0.45rem;
  color: var(--color-gold-dark);
  line-height: 1;
}

.hero__families {
  font-family: var(--font-sans);
  font-size: 0.64rem;
  font-weight: 600;
  letter-spacing: 0.32em;
  text-transform: uppercase;
  color: var(--color-gold-dark);
  margin-top: 0.4rem;
  text-shadow: 0 1px 4px rgba(255, 255, 255, 0.9);
  opacity: 0;
  transform: translateY(-10px);
}

.hero__names-wrap {
  margin-top: 0.35rem;
  opacity: 0;
  transform: translateY(15px);
}

.hero__names {
  font-family: var(--font-cursive);
  font-size: clamp(2.9rem, 9.5vw, 3.7rem);
  font-weight: 400;
  color: #3b1016;
  text-shadow: 0 2px 14px rgba(255, 255, 255, 0.95), 0 1px 3px rgba(74, 20, 26, 0.18);
  line-height: 1.15;
  white-space: nowrap;
}

.hero__amp {
  display: inline-block;
  font-family: var(--font-serif);
  font-style: italic;
  font-size: 0.78em;
  color: var(--color-gold-dark);
  margin: 0 0.2rem;
  text-shadow: 0 1px 6px rgba(255, 255, 255, 0.9);
}

/* Ornamental divider */
.hero__ornament {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  margin: 0.6rem auto;
  opacity: 0;
  transform: translateY(10px);
}

.hero__orn-line {
  width: 45px;
  height: 1px;
  background: linear-gradient(90deg, transparent, var(--color-gold-dark), transparent);
}

.hero__orn-diamond {
  font-size: 0.38rem;
  color: var(--color-gold-dark);
}

/* Date */
.hero__date {
  font-family: var(--font-serif);
  font-size: 1.05rem;
  font-weight: 600;
  letter-spacing: 0.25em;
  color: #4a141a;
  text-shadow: 0 1px 8px rgba(255, 255, 255, 0.9);
  opacity: 0;
  transform: translateY(10px);
}

/* ── Bottom Content ── */
.hero__footer {
  position: relative;
  z-index: 2;
  text-align: center;
  width: 100%;
  max-width: 420px;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 0.25rem;
}

.hero__badge-wrap {
  opacity: 0;
  transform: translateY(15px);
}

.hero__venue-hint {
  font-family: var(--font-sans);
  font-size: 0.62rem;
  font-weight: 600;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  color: #4a141a;
  background: rgba(255, 255, 255, 0.72);
  padding: 0.45rem 1rem;
  border-radius: 20px;
  backdrop-filter: blur(6px);
  border: 1px solid rgba(212, 175, 55, 0.3);
  box-shadow: 0 2px 10px rgba(74, 20, 26, 0.08);
  max-width: 290px;
  line-height: 1.5;
}

/* Scroll hint */
.hero__scroll-hint {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.2rem;
  color: #4a141a;
  margin-top: 0.75rem;
  opacity: 0;
  transform: translateY(10px);
  cursor: pointer;
}

.hero__scroll-hint span {
  font-family: var(--font-sans);
  font-size: 0.52rem;
  font-weight: 600;
  letter-spacing: 0.22em;
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
  height: 40px;
  background: linear-gradient(to bottom, transparent, var(--color-warm-gray));
  z-index: 1;
}

/* Animation trigger class */
.hero__animate {
  animation: fadeInUp 0.8s cubic-bezier(0.16, 1, 0.3, 1) forwards;
  animation-delay: var(--delay, 0s);
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(15px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes bounceSoft {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(4px);
  }
}
</style>
