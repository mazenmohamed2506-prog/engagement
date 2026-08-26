<template>
  <section class="hero" id="hero">
    <!-- Top & bottom lighting gradients to preserve photo faces clearly -->
    <div class="hero__overlay-top"></div>
    <div class="hero__overlay-bottom"></div>

    <!-- Top header: positioned above the faces -->
    <div class="hero__header">
      <div class="hero__top-decor" :class="{ 'hero__animate': animate }" style="--delay: 0.1s">
        <span class="hero__decor-line"></span>
        <span class="hero__decor-diamond">✦</span>
        <span class="hero__decor-line"></span>
      </div>

      <p class="hero__families" :class="{ 'hero__animate': animate }" style="--delay: 0.3s">
        Together with their families
      </p>
    </div>

    <!-- Bottom content: positioned below faces over natural dress/suit area -->
    <div class="hero__footer">
      <div class="hero__names-wrap" :class="{ 'hero__animate': animate }" style="--delay: 0.6s">
        <h1 class="hero__names">
          Mohamed <span class="hero__amp">&</span> Asmaa
        </h1>
      </div>

      <div class="hero__ornament" :class="{ 'hero__animate': animate }" style="--delay: 0.8s">
        <span class="hero__orn-line"></span>
        <span class="hero__orn-diamond">◆</span>
        <span class="hero__orn-line"></span>
      </div>

      <p class="hero__date" :class="{ 'hero__animate': animate }" style="--delay: 1s">
        26 &nbsp;|&nbsp; 09 &nbsp;|&nbsp; 2026
      </p>

      <p class="hero__venue-hint" :class="{ 'hero__animate': animate }" style="--delay: 1.2s">
        Request the honour of your presence at our wedding
      </p>

      <div class="hero__scroll-hint" :class="{ 'hero__animate': animate }" style="--delay: 1.5s">
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
  background-position: center 15%;
  overflow: hidden;
  padding: 2.5rem 1.5rem 1.75rem;
}

/* Subtle top gradient for legible header */
.hero__overlay-top {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 28%;
  background: linear-gradient(
    to bottom,
    rgba(40, 12, 18, 0.75) 0%,
    rgba(40, 12, 18, 0.35) 50%,
    transparent 100%
  );
  pointer-events: none;
  z-index: 1;
}

/* Deep smooth gradient at bottom to frame typography */
.hero__overlay-bottom {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 52%;
  background: linear-gradient(
    to top,
    rgba(35, 10, 15, 0.96) 0%,
    rgba(35, 10, 15, 0.85) 30%,
    rgba(35, 10, 15, 0.5) 65%,
    transparent 100%
  );
  pointer-events: none;
  z-index: 1;
}

/* ── Top Header ── */
.hero__header {
  position: relative;
  z-index: 2;
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
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
  background: linear-gradient(90deg, transparent, var(--color-gold), transparent);
}

.hero__decor-diamond {
  font-size: 0.45rem;
  color: var(--color-gold-light);
  line-height: 1;
}

.hero__families {
  font-family: var(--font-sans);
  font-size: 0.62rem;
  font-weight: 500;
  letter-spacing: 0.35em;
  text-transform: uppercase;
  color: #f9f6f0;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.7);
  opacity: 0;
  transform: translateY(-10px);
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
  margin-bottom: 0.5rem;
}

.hero__names-wrap {
  opacity: 0;
  transform: translateY(20px);
}

.hero__names {
  font-family: var(--font-cursive);
  font-size: clamp(2.6rem, 8.5vw, 3.4rem);
  font-weight: 400;
  color: #ffffff;
  text-shadow: 0 4px 20px rgba(0, 0, 0, 0.7), 0 2px 6px rgba(0, 0, 0, 0.8);
  line-height: 1.15;
  white-space: nowrap;
}

.hero__amp {
  display: inline-block;
  font-family: var(--font-serif);
  font-style: italic;
  font-size: 0.75em;
  color: var(--color-gold-light);
  margin: 0 0.2rem;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.7);
}

/* Ornamental divider */
.hero__ornament {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  margin: 0.75rem auto;
  opacity: 0;
  transform: translateY(15px);
}

.hero__orn-line {
  width: 45px;
  height: 1px;
  background: linear-gradient(90deg, transparent, var(--color-gold), transparent);
}

.hero__orn-diamond {
  font-size: 0.38rem;
  color: var(--color-gold-light);
}

/* Date */
.hero__date {
  font-family: var(--font-serif);
  font-size: 1.05rem;
  font-weight: 400;
  letter-spacing: 0.25em;
  color: #ffffff;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.7);
  opacity: 0;
  transform: translateY(15px);
}

/* Venue hint */
.hero__venue-hint {
  font-family: var(--font-sans);
  font-size: 0.6rem;
  font-weight: 400;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--color-gold-light);
  margin-top: 0.75rem;
  text-shadow: 0 2px 8px rgba(0, 0, 0, 0.7);
  max-width: 280px;
  line-height: 1.6;
  opacity: 0;
  transform: translateY(15px);
}

/* Scroll hint */
.hero__scroll-hint {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.25rem;
  color: rgba(244, 239, 234, 0.7);
  margin-top: 1.25rem;
  opacity: 0;
  transform: translateY(10px);
  cursor: pointer;
}

.hero__scroll-hint span {
  font-family: var(--font-sans);
  font-size: 0.52rem;
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
  height: 60px;
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
</style>
