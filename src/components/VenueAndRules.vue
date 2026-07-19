<template>
  <section class="venue-rules" id="venue">
    <div class="venue-rules__inner">
      <!-- Venue Section -->
      <h2 class="venue-rules__heading">The Venue</h2>

      <svg class="venue-rules__divider" viewBox="0 0 200 20" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M0 10 Q25 0 50 10 Q75 20 100 10 Q125 0 150 10 Q175 20 200 10" stroke="currentColor" stroke-width="1" fill="none" opacity="0.5"/>
        <circle cx="100" cy="10" r="3" fill="currentColor" opacity="0.6"/>
        <line x1="60" y1="10" x2="85" y2="10" stroke="currentColor" stroke-width="0.5" opacity="0.4"/>
        <line x1="115" y1="10" x2="140" y2="10" stroke="currentColor" stroke-width="0.5" opacity="0.4"/>
      </svg>

      <!-- 3D Flip Card -->
      <div class="flip-card" @click="isFlipped = !isFlipped">
        <div class="flip-card__inner" :class="{ 'flip-card__inner--flipped': isFlipped }">
          <!-- Front: Venue Image -->
          <div class="flip-card__face flip-card__front">
            <div class="flip-card__arch">
              <img :src="venueImg" alt="Wedding venue" class="flip-card__image" />
              <div class="flip-card__overlay">
                <p class="flip-card__venue-name">Seaside Terrace</p>
                <p class="flip-card__venue-location">Alexandria, Egypt</p>
              </div>
            </div>
            <p class="flip-card__hint">Tap to see location</p>
          </div>

          <!-- Back: QR Code -->
          <div class="flip-card__face flip-card__back">
            <div class="flip-card__qr-content">
              <p class="flip-card__qr-title">Scan for Directions</p>
              <div class="flip-card__qr-frame">
                <img :src="qrCode" alt="Venue QR code" class="flip-card__qr-image" />
              </div>
              <p class="flip-card__qr-subtitle">Point your camera at the QR code</p>
            </div>
            <p class="flip-card__hint flip-card__hint--back">Tap to flip back</p>
          </div>
        </div>
      </div>

      <!-- Rules Section -->
      <h2 class="venue-rules__heading venue-rules__heading--rules">Kind Reminders</h2>

      <div class="rules">
        <div class="rules__card">
          <div class="rules__icon">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
              <path d="M6 2L3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4z" />
              <line x1="3" y1="6" x2="21" y2="6" />
              <path d="M16 10a4 4 0 0 1-8 0" />
            </svg>
          </div>
          <h3 class="rules__title">Dress Code</h3>
          <p class="rules__desc">Formal Elegant Attire<br/><span class="rules__subdesc">Ladies: long dresses preferred<br/>Gentlemen: suit & tie</span></p>
        </div>

        <div class="rules__card">
          <div class="rules__icon">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
              <path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2" />
              <circle cx="9" cy="7" r="4" />
              <path d="M23 21v-2a4 4 0 0 0-3-3.87" />
              <path d="M16 3.13a4 4 0 0 1 0 7.75" />
            </svg>
          </div>
          <h3 class="rules__title">Adults Only</h3>
          <p class="rules__desc">We kindly request that this<br/>celebration be an adults-only event</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'
import venueImg from '@/assets/images/venue.png'
import qrCode from '@/assets/images/qr-code.png'

const isFlipped = ref(false)
</script>

<style scoped>
.venue-rules {
  padding: 4rem 1.5rem;
  background: var(--color-warm-gray);
}

.venue-rules__inner {
  max-width: 400px;
  margin: 0 auto;
}

.venue-rules__heading {
  font-family: var(--font-serif);
  font-size: 1.75rem;
  font-weight: 500;
  color: var(--color-navy);
  text-align: center;
  margin-bottom: 0.75rem;
}

.venue-rules__heading--rules {
  margin-top: 3rem;
}

.venue-rules__divider {
  display: block;
  width: 140px;
  height: 20px;
  margin: 0 auto 2rem;
  color: var(--color-gold);
}

/* ── Flip Card ── */
.flip-card {
  perspective: 1000px;
  cursor: pointer;
  margin: 0 auto;
  max-width: 300px;
}

.flip-card__inner {
  position: relative;
  width: 100%;
  aspect-ratio: 3 / 4;
  transition: transform 0.8s cubic-bezier(0.4, 0, 0.2, 1);
  transform-style: preserve-3d;
}

.flip-card__inner--flipped {
  transform: rotateY(180deg);
}

.flip-card__face {
  position: absolute;
  inset: 0;
  backface-visibility: hidden;
  border-radius: 12px;
  overflow: hidden;
}

.flip-card__front {
  display: flex;
  flex-direction: column;
}

.flip-card__arch {
  position: relative;
  flex: 1;
  border-radius: 200px 200px 0 0;
  overflow: hidden;
}

.flip-card__image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.flip-card__overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 2rem 1.5rem;
  background: linear-gradient(to top, rgba(26, 39, 68, 0.8), transparent);
  text-align: center;
}

.flip-card__venue-name {
  font-family: var(--font-serif);
  font-size: 1.25rem;
  font-weight: 500;
  color: #fff;
}

.flip-card__venue-location {
  font-family: var(--font-sans);
  font-size: 0.7rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--color-gold-light);
  margin-top: 0.25rem;
}

.flip-card__hint {
  font-family: var(--font-sans);
  font-size: 0.6rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--color-navy-light);
  text-align: center;
  padding: 0.75rem 0;
  opacity: 0.6;
}

.flip-card__hint--back {
  color: var(--color-gold-dark);
}

/* Back face */
.flip-card__back {
  transform: rotateY(180deg);
  background: linear-gradient(160deg, var(--color-navy), var(--color-navy-dark));
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.flip-card__qr-content {
  text-align: center;
  padding: 2rem;
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.flip-card__qr-title {
  font-family: var(--font-serif);
  font-size: 1.1rem;
  color: var(--color-ivory);
  margin-bottom: 1.5rem;
}

.flip-card__qr-frame {
  width: 160px;
  height: 160px;
  padding: 12px;
  background: white;
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
}

.flip-card__qr-image {
  width: 100%;
  height: 100%;
  object-fit: contain;
}

.flip-card__qr-subtitle {
  font-family: var(--font-sans);
  font-size: 0.65rem;
  letter-spacing: 0.1em;
  color: var(--color-gold-light);
  margin-top: 1.25rem;
  opacity: 0.7;
}

/* ── Rules ── */
.rules {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  margin-top: 1.5rem;
}

.rules__card {
  background: var(--color-ivory);
  border-radius: 8px;
  padding: 1.5rem;
  text-align: center;
  box-shadow: 0 2px 12px rgba(26, 39, 68, 0.06);
  border: 1px solid var(--color-warm-gray-dark);
}

.rules__icon {
  width: 44px;
  height: 44px;
  margin: 0 auto 1rem;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--color-gold);
}

.rules__icon svg {
  width: 28px;
  height: 28px;
}

.rules__title {
  font-family: var(--font-serif);
  font-size: 1.1rem;
  font-weight: 500;
  color: var(--color-navy);
  margin-bottom: 0.5rem;
}

.rules__desc {
  font-family: var(--font-sans);
  font-size: 0.78rem;
  color: var(--color-navy-light);
  line-height: 1.6;
}

.rules__subdesc {
  font-size: 0.7rem;
  opacity: 0.6;
}
</style>
