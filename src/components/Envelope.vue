<template>
  <div v-if="!dismissed" class="envelope" :class="{ 'envelope--opened': isOpened }">
    <!-- Envelope Back -->
    <div class="envelope__back"></div>

    <!-- Envelope Side Flaps -->
    <div class="envelope__flap-left"></div>
    <div class="envelope__flap-right"></div>

    <!-- Bottom Flap -->
    <div class="envelope__flap-bottom"></div>

    <!-- Inner Card (the invitation preview) -->
    <div class="envelope__card" :class="{ 'envelope__card--revealed': isOpened }">
      <div class="envelope__card-inner">
        <p class="envelope__card-top">You Are Invited</p>
        <h2 class="envelope__card-names">Omar & Mariyem</h2>
        <div class="envelope__card-divider"></div>
        <p class="envelope__card-date">30 · 07 · 2026</p>
      </div>
    </div>

    <!-- Top Flap (opens on click) -->
    <div class="envelope__flap-top" :class="{ 'envelope__flap-top--open': isOpened }"></div>

    <!-- Seal Button -->
    <button
      v-if="!isOpened"
      class="envelope__seal"
      @click="openEnvelope"
      aria-label="Open invitation"
    >
      <svg viewBox="0 0 60 60" class="envelope__seal-icon">
        <!-- Seashell design -->
        <circle cx="30" cy="30" r="28" fill="none" stroke="currentColor" stroke-width="1"/>
        <path d="M30 10 C20 20, 15 35, 30 50 C45 35, 40 20, 30 10Z" fill="none" stroke="currentColor" stroke-width="1"/>
        <path d="M30 10 C25 25, 22 40, 30 50" fill="none" stroke="currentColor" stroke-width="0.8" opacity="0.6"/>
        <path d="M30 10 C35 25, 38 40, 30 50" fill="none" stroke="currentColor" stroke-width="0.8" opacity="0.6"/>
        <line x1="30" y1="14" x2="30" y2="46" stroke="currentColor" stroke-width="0.5" opacity="0.4"/>
        <text x="30" y="34" text-anchor="middle" font-size="8" fill="currentColor" font-family="var(--font-serif)">Open</text>
      </svg>
    </button>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const emit = defineEmits(['opened'])
const isOpened = ref(false)
const dismissed = ref(false)

function openEnvelope() {
  isOpened.value = true

  // After the full animation, emit opened and dismiss
  setTimeout(() => {
    emit('opened')
    setTimeout(() => {
      dismissed.value = true
    }, 500)
  }, 2200)
}
</script>

<style scoped>
.envelope {
  position: fixed;
  inset: 0;
  z-index: 500;
  display: flex;
  align-items: center;
  justify-content: center;
  perspective: 1200px;
  background: var(--color-ivory);
  transition: opacity 0.5s ease 2s;
}

.envelope--opened {
  pointer-events: none;
  opacity: 0;
}

/* Envelope body */
.envelope__back {
  position: absolute;
  width: 85%;
  max-width: 340px;
  height: 55vh;
  max-height: 420px;
  background: linear-gradient(145deg, var(--color-navy), var(--color-navy-dark));
  border-radius: 8px;
  box-shadow: 0 20px 60px rgba(26, 39, 68, 0.4);
}

/* Side flaps */
.envelope__flap-left,
.envelope__flap-right {
  position: absolute;
  width: 0;
  height: 0;
}

.envelope__flap-left {
  top: 50%;
  left: calc(50% - 170px);
  transform: translateY(-50%);
  border-top: 130px solid transparent;
  border-bottom: 130px solid transparent;
  border-left: 100px solid var(--color-navy-light);
}

.envelope__flap-right {
  top: 50%;
  right: calc(50% - 170px);
  transform: translateY(-50%);
  border-top: 130px solid transparent;
  border-bottom: 130px solid transparent;
  border-right: 100px solid var(--color-navy-light);
}

/* Bottom flap */
.envelope__flap-bottom {
  position: absolute;
  width: 0;
  height: 0;
  bottom: calc(50% - 210px);
  left: 50%;
  transform: translateX(-50%);
  border-left: 170px solid transparent;
  border-right: 170px solid transparent;
  border-bottom: 140px solid #1e2f52;
}

/* Top flap */
.envelope__flap-top {
  position: absolute;
  width: 0;
  height: 0;
  top: calc(50% - 210px);
  left: 50%;
  transform: translateX(-50%);
  border-left: 170px solid transparent;
  border-right: 170px solid transparent;
  border-top: 160px solid var(--color-navy);
  z-index: 10;
  transform-origin: top center;
  transition: transform 0.8s ease-in-out;
  filter: drop-shadow(0 4px 8px rgba(0, 0, 0, 0.2));
}

.envelope__flap-top--open {
  transform: translateX(-50%) rotateX(180deg);
}

/* Inner card */
.envelope__card {
  position: absolute;
  width: 75%;
  max-width: 290px;
  height: 45vh;
  max-height: 350px;
  background: linear-gradient(160deg, var(--color-ivory), #fff, var(--color-ivory-dark));
  border-radius: 6px;
  z-index: 5;
  display: flex;
  align-items: center;
  justify-content: center;
  transform: translateY(80%) scale(0.8);
  opacity: 0;
  transition: transform 1.2s cubic-bezier(0.34, 1.56, 0.64, 1) 0.6s,
              opacity 0.8s ease 0.6s,
              z-index 0s linear 0.6s;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.15);
  border: 1px solid var(--color-gold-light);
}

.envelope__card--revealed {
  transform: translateY(0) scale(1);
  opacity: 1;
  z-index: 520;
}

.envelope__card-inner {
  text-align: center;
  padding: 2rem;
}

.envelope__card-top {
  font-family: var(--font-sans);
  font-size: 0.65rem;
  letter-spacing: 0.35em;
  text-transform: uppercase;
  color: var(--color-gold-dark);
  margin-bottom: 1rem;
}

.envelope__card-names {
  font-family: var(--font-cursive);
  font-size: 2.5rem;
  color: var(--color-navy);
  line-height: 1.2;
  margin-bottom: 1rem;
}

.envelope__card-divider {
  width: 50px;
  height: 1px;
  background: var(--color-gold);
  margin: 0 auto 1rem;
}

.envelope__card-date {
  font-family: var(--font-serif);
  font-size: 1rem;
  color: var(--color-navy-light);
  letter-spacing: 0.15em;
}

/* Seal button */
.envelope__seal {
  position: absolute;
  z-index: 15;
  width: 68px;
  height: 68px;
  border-radius: 50%;
  border: 2px solid var(--color-gold);
  background: radial-gradient(circle at 30% 30%, var(--color-gold-light), var(--color-gold), var(--color-gold-dark));
  color: var(--color-navy);
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  box-shadow: 0 4px 20px rgba(201, 169, 110, 0.4);
  animation: pulseSoft 2s ease-in-out infinite;
}

.envelope__seal:hover {
  transform: scale(1.1);
  box-shadow: 0 6px 30px rgba(201, 169, 110, 0.6);
}

.envelope__seal-icon {
  width: 44px;
  height: 44px;
}

/* Responsive adjustments */
@media (max-width: 380px) {
  .envelope__back {
    width: 90%;
    height: 50vh;
  }

  .envelope__flap-left {
    left: calc(50% - 48%);
    border-left-width: 80px;
    border-top-width: 110px;
    border-bottom-width: 110px;
  }

  .envelope__flap-right {
    right: calc(50% - 48%);
    border-right-width: 80px;
    border-top-width: 110px;
    border-bottom-width: 110px;
  }

  .envelope__card-names {
    font-size: 2rem;
  }
}
</style>
