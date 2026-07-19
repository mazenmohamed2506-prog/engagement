<template>
  <section class="countdown" id="countdown">
    <div class="countdown__inner">
      <h2 class="countdown__heading">Counting the Moments</h2>

      <!-- SVG Divider -->
      <svg class="countdown__divider" viewBox="0 0 200 20" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M0 10 Q25 0 50 10 Q75 20 100 10 Q125 0 150 10 Q175 20 200 10" stroke="currentColor" stroke-width="1" fill="none" opacity="0.5"/>
        <circle cx="100" cy="10" r="3" fill="currentColor" opacity="0.6"/>
        <line x1="60" y1="10" x2="85" y2="10" stroke="currentColor" stroke-width="0.5" opacity="0.4"/>
        <line x1="115" y1="10" x2="140" y2="10" stroke="currentColor" stroke-width="0.5" opacity="0.4"/>
      </svg>

      <div class="countdown__timer">
        <div class="countdown__block">
          <span class="countdown__number">{{ days }}</span>
          <span class="countdown__label">Days</span>
        </div>

        <span class="countdown__separator">:</span>

        <div class="countdown__block">
          <span class="countdown__number">{{ hours }}</span>
          <span class="countdown__label">Hours</span>
        </div>

        <span class="countdown__separator">:</span>

        <div class="countdown__block">
          <span class="countdown__number">{{ minutes }}</span>
          <span class="countdown__label">Minutes</span>
        </div>
      </div>

      <p class="countdown__date-label">August 2, 2026</p>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const targetDate = new Date('2026-08-02T16:00:00').getTime()

const days = ref('00')
const hours = ref('00')
const minutes = ref('00')
let intervalId = null

function pad(n) {
  return String(n).padStart(2, '0')
}

function updateCountdown() {
  const now = Date.now()
  const diff = targetDate - now

  if (diff <= 0) {
    days.value = '00'
    hours.value = '00'
    minutes.value = '00'
    if (intervalId) clearInterval(intervalId)
    return
  }

  const d = Math.floor(diff / (1000 * 60 * 60 * 24))
  const h = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60))
  const m = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60))

  days.value = pad(d)
  hours.value = pad(h)
  minutes.value = pad(m)
}

onMounted(() => {
  updateCountdown()
  intervalId = setInterval(updateCountdown, 1000)
})

onUnmounted(() => {
  if (intervalId) clearInterval(intervalId)
})
</script>

<style scoped>
.countdown {
  background: var(--color-ivory);
  padding: 4rem 1.5rem;
}

.countdown__inner {
  text-align: center;
  max-width: 400px;
  margin: 0 auto;
}

.countdown__heading {
  font-family: var(--font-serif);
  font-size: 1.75rem;
  font-weight: 500;
  color: var(--color-navy);
  margin-bottom: 0.75rem;
}

.countdown__divider {
  width: 140px;
  height: 20px;
  margin: 0 auto 2.5rem;
  color: var(--color-gold);
}

.countdown__timer {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
}

.countdown__block {
  display: flex;
  flex-direction: column;
  align-items: center;
  min-width: 70px;
  padding: 1rem 0.75rem;
  background: white;
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(26, 39, 68, 0.08);
  border: 1px solid var(--color-warm-gray);
}

.countdown__number {
  font-family: var(--font-serif);
  font-size: 2.5rem;
  font-weight: 600;
  color: var(--color-navy);
  line-height: 1;
}

.countdown__label {
  font-family: var(--font-sans);
  font-size: 0.6rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--color-gold-dark);
  margin-top: 0.5rem;
}

.countdown__separator {
  font-family: var(--font-serif);
  font-size: 2rem;
  color: var(--color-gold);
  margin-top: -1rem;
}

.countdown__date-label {
  font-family: var(--font-serif);
  font-style: italic;
  font-size: 0.9rem;
  color: var(--color-navy-light);
  margin-top: 2rem;
  opacity: 0.7;
}
</style>
