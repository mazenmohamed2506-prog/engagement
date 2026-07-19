<template>
  <div v-if="!dismissed" class="envelope-screen" :class="{ 'envelope-screen--fading': isFading }">
    <!-- Decorative particles -->
    <div class="envelope-screen__particles">
      <span v-for="n in 20" :key="n" class="particle" :style="particleStyle(n)"></span>
    </div>

    <!-- Top decorative text -->
    <p class="envelope-screen__pretext" :class="{ 'animate-in': showElements }">
      You have received an invitation
    </p>

    <!-- The Envelope -->
    <div class="envelope" :class="{ 'envelope--opened': isOpened }">
      <!-- Envelope body (back) -->
      <div class="envelope__body">
        <div class="envelope__texture"></div>
      </div>

      <!-- Top flap -->
      <div class="envelope__flap" :class="{ 'envelope__flap--open': isOpened }">
        <div class="envelope__flap-texture"></div>
        <div class="envelope__flap-shadow"></div>
      </div>

      <!-- Inner invitation card -->
      <div class="envelope__card" :class="{ 'envelope__card--revealed': isOpened }">
        <div class="envelope__card-border">
          <img :src="floralFrame" alt="" class="envelope__card-frame" />
          <div class="envelope__card-content">
            <p class="envelope__card-top">You Are Cordially Invited</p>
            <p class="envelope__card-to">to the engagement of</p>
            <h2 class="envelope__card-names">Omar & Mariyem</h2>
            <div class="envelope__card-ornament">
              <span class="ornament-line"></span>
              <span class="ornament-diamond">◆</span>
              <span class="ornament-line"></span>
            </div>
            <p class="envelope__card-date">30 · 07 · 2026</p>
            <p class="envelope__card-day">Thursday Evening</p>
          </div>
        </div>
      </div>

      <!-- Bottom flap (covers bottom of card) -->
      <div class="envelope__bottom-flap"></div>
    </div>

    <!-- Seal / Open Button -->
    <button
      v-if="!isOpened"
      class="envelope-screen__seal"
      :class="{ 'animate-in': showElements }"
      @click="openEnvelope"
      aria-label="Open invitation"
    >
      <div class="seal__inner">
        <div class="seal__ring"></div>
        <span class="seal__text">Open</span>
      </div>
    </button>

    <!-- Bottom text -->
    <p v-if="!isOpened" class="envelope-screen__hint" :class="{ 'animate-in': showElements }">
      Tap the seal to open
    </p>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import floralFrame from '@/assets/images/floral-frame.png'

const emit = defineEmits(['opened'])
const isOpened = ref(false)
const isFading = ref(false)
const dismissed = ref(false)
const showElements = ref(false)

onMounted(() => {
  setTimeout(() => {
    showElements.value = true
  }, 300)
})

function particleStyle(n) {
  const x = Math.random() * 100
  const y = Math.random() * 100
  const size = 2 + Math.random() * 4
  const delay = Math.random() * 5
  const duration = 3 + Math.random() * 4
  return {
    left: `${x}%`,
    top: `${y}%`,
    width: `${size}px`,
    height: `${size}px`,
    animationDelay: `${delay}s`,
    animationDuration: `${duration}s`,
  }
}

function openEnvelope() {
  isOpened.value = true

  setTimeout(() => {
    isFading.value = true
    setTimeout(() => {
      emit('opened')
      dismissed.value = true
    }, 800)
  }, 2400)
}
</script>

<style scoped>
.envelope-screen {
  position: fixed;
  inset: 0;
  z-index: 500;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 2rem;
  background: linear-gradient(160deg, var(--color-warm-gray-dark), var(--color-ivory), var(--color-warm-gray));
  overflow: hidden;
  transition: opacity 0.8s ease;
}

.envelope-screen--fading {
  opacity: 0;
  pointer-events: none;
}

/* ── Particles ── */
.envelope-screen__particles {
  position: absolute;
  inset: 0;
  pointer-events: none;
}

.particle {
  position: absolute;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(201, 169, 110, 0.4), transparent);
  animation: particleFloat var(--duration, 4s) ease-in-out infinite alternate;
}

@keyframes particleFloat {
  0% { opacity: 0; transform: translateY(0) scale(0.5); }
  50% { opacity: 0.6; }
  100% { opacity: 0; transform: translateY(-40px) scale(1.2); }
}

/* ── Pre-text ── */
.envelope-screen__pretext {
  font-family: var(--font-sans);
  font-size: 0.65rem;
  letter-spacing: 0.4em;
  text-transform: uppercase;
  color: var(--color-navy-light);
  opacity: 0;
  transform: translateY(10px);
  transition: all 0.8s ease 0.2s;
  text-align: center;
}

.envelope-screen__pretext.animate-in {
  opacity: 0.8;
  transform: translateY(0);
}

/* ── Envelope ── */
.envelope {
  position: relative;
  width: 300px;
  height: 400px;
  perspective: 800px;
}

/* Envelope body */
.envelope__body {
  position: absolute;
  inset: 0;
  background: linear-gradient(165deg, var(--color-navy-light), var(--color-navy), var(--color-navy-dark));
  border-radius: 6px;
  box-shadow:
    0 25px 50px rgba(0, 0, 0, 0.15),
    0 10px 20px rgba(0, 0, 0, 0.1);
  overflow: hidden;
}

.envelope__texture {
  position: absolute;
  inset: 0;
  background-image: url('@/assets/images/envelope-bg.png');
  background-size: cover;
  background-position: center;
  opacity: 0.9;
}

/* Gold border trim */
.envelope__body::before {
  content: '';
  position: absolute;
  inset: 8px;
  border: 1px solid rgba(201, 169, 110, 0.4);
  border-radius: 4px;
  pointer-events: none;
}

/* Top flap */
.envelope__flap {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 200px;
  z-index: 20;
  transform-origin: top center;
  transform-style: preserve-3d;
  transition: transform 1s cubic-bezier(0.4, 0, 0.2, 1);
}

.envelope__flap::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 100%;
  background: linear-gradient(180deg, var(--color-navy-light), var(--color-navy));
  clip-path: polygon(0 0, 100% 0, 50% 100%);
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
}

.envelope__flap-texture {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 100%;
  clip-path: polygon(0 0, 100% 0, 50% 100%);
  background-image: url('@/assets/images/envelope-bg.png');
  background-size: cover;
  background-position: top center;
  opacity: 0.9;
}

/* Gold edge on flap */
.envelope__flap::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 100%;
  clip-path: polygon(0 0, 100% 0, 50% 100%);
  border: 1.5px solid rgba(201, 169, 110, 0.3);
  pointer-events: none;
}

.envelope__flap--open {
  transform: rotateX(180deg);
}

.envelope__flap-shadow {
  position: absolute;
  bottom: -20px;
  left: 10%;
  right: 10%;
  height: 20px;
  background: linear-gradient(to bottom, rgba(0, 0, 0, 0.1), transparent);
  transition: opacity 0.5s ease;
}

.envelope__flap--open .envelope__flap-shadow {
  opacity: 0;
}

/* Bottom flap */
.envelope__bottom-flap {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 180px;
  background: linear-gradient(0deg, var(--color-navy-dark), var(--color-navy));
  clip-path: polygon(0 100%, 100% 100%, 50% 0);
  z-index: 6;
}

.envelope__bottom-flap::before {
  content: '';
  position: absolute;
  inset: 0;
  background-image: url('@/assets/images/envelope-bg.png');
  background-size: cover;
  background-position: bottom center;
  opacity: 0.9;
  clip-path: polygon(0 100%, 100% 100%, 50% 0);
}

.envelope__bottom-flap::after {
  content: '';
  position: absolute;
  inset: 0;
  clip-path: polygon(0 100%, 100% 100%, 50% 0);
  border: 1.5px solid rgba(201, 169, 110, 0.2);
}

/* ── Inner Card ── */
.envelope__card {
  position: absolute;
  top: 30px;
  left: 20px;
  right: 20px;
  bottom: 30px;
  z-index: 5;
  transform: translateY(0) scale(0.85);
  opacity: 0;
  transition:
    transform 1.4s cubic-bezier(0.34, 1.56, 0.64, 1) 0.8s,
    opacity 0.6s ease 0.8s,
    z-index 0s linear 0.8s;
}

.envelope__card--revealed {
  transform: translateY(-120px) scale(1.05);
  opacity: 1;
  z-index: 30;
}

.envelope__card-border {
  width: 100%;
  height: 100%;
  background: linear-gradient(170deg, #fffef9, #faf7f0, #f5f0e5);
  border-radius: 8px;
  padding: 1rem;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  box-shadow:
    0 15px 50px rgba(0, 0, 0, 0.3),
    0 5px 15px rgba(0, 0, 0, 0.15),
    inset 0 0 0 1px rgba(201, 169, 110, 0.3);
  overflow: hidden;
}

.envelope__card-frame {
  position: absolute;
  inset: 5px;
  width: calc(100% - 10px);
  height: calc(100% - 10px);
  object-fit: contain;
  opacity: 0.4;
  pointer-events: none;
}

.envelope__card-content {
  text-align: center;
  position: relative;
  z-index: 2;
}

.envelope__card-top {
  font-family: var(--font-sans);
  font-size: 0.55rem;
  letter-spacing: 0.4em;
  text-transform: uppercase;
  color: var(--color-gold-dark);
  margin-bottom: 0.5rem;
}

.envelope__card-to {
  font-family: var(--font-serif);
  font-size: 0.8rem;
  font-style: italic;
  color: var(--color-navy-light);
  margin-bottom: 0.75rem;
}

.envelope__card-names {
  font-family: var(--font-cursive);
  font-size: 2.2rem;
  color: var(--color-navy);
  line-height: 1.2;
  margin-bottom: 0.75rem;
  text-shadow: 0 1px 2px rgba(26, 39, 68, 0.1);
}

.envelope__card-ornament {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  margin-bottom: 0.75rem;
}

.ornament-line {
  width: 35px;
  height: 1px;
  background: linear-gradient(90deg, transparent, var(--color-gold), transparent);
}

.ornament-diamond {
  font-size: 0.45rem;
  color: var(--color-gold);
}

.envelope__card-date {
  font-family: var(--font-serif);
  font-size: 0.95rem;
  color: var(--color-navy);
  letter-spacing: 0.2em;
}

.envelope__card-day {
  font-family: var(--font-sans);
  font-size: 0.6rem;
  letter-spacing: 0.3em;
  text-transform: uppercase;
  color: var(--color-gold-dark);
  margin-top: 0.35rem;
}

/* ── Seal Button ── */
.envelope-screen__seal {
  position: relative;
  z-index: 100;
  width: 80px;
  height: 80px;
  border-radius: 50%;
  border: none;
  background: radial-gradient(ellipse at 35% 30%,
    #e8c97a,
    #c9a96e 40%,
    #a8894e 70%,
    #8a6d3b
  );
  cursor: pointer;
  transition: transform 0.4s ease, box-shadow 0.4s ease;
  box-shadow:
    0 4px 20px rgba(201, 169, 110, 0.4),
    0 8px 40px rgba(0, 0, 0, 0.3),
    inset 0 -2px 4px rgba(0, 0, 0, 0.2),
    inset 0 2px 4px rgba(255, 255, 255, 0.3);
  opacity: 0;
  transform: translateY(10px) scale(0.9);
  transition: all 0.8s ease 0.6s;
  margin-top: -1rem;
}

.envelope-screen__seal.animate-in {
  opacity: 1;
  transform: translateY(0) scale(1);
}

.envelope-screen__seal:hover {
  transform: scale(1.12) !important;
  box-shadow:
    0 6px 30px rgba(201, 169, 110, 0.6),
    0 12px 50px rgba(0, 0, 0, 0.3),
    inset 0 -2px 4px rgba(0, 0, 0, 0.2),
    inset 0 2px 4px rgba(255, 255, 255, 0.3);
}

.seal__inner {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  position: relative;
}

.seal__ring {
  position: absolute;
  inset: 6px;
  border-radius: 50%;
  border: 1.5px solid rgba(255, 255, 255, 0.25);
}

.seal__text {
  font-family: var(--font-serif);
  font-size: 0.8rem;
  font-weight: 500;
  color: var(--color-navy-dark);
  letter-spacing: 0.15em;
  text-transform: uppercase;
}

/* ── Hint Text ── */
.envelope-screen__hint {
  font-family: var(--font-sans);
  font-size: 0.6rem;
  letter-spacing: 0.25em;
  text-transform: uppercase;
  color: rgba(201, 169, 110, 0.4);
  opacity: 0;
  transform: translateY(5px);
  transition: all 0.6s ease 1s;
}

.envelope-screen__hint.animate-in {
  opacity: 1;
  transform: translateY(0);
}

/* ── Responsive ── */
@media (max-width: 360px) {
  .envelope {
    width: 260px;
    height: 350px;
  }

  .envelope__card-names {
    font-size: 1.8rem;
  }
}
</style>
