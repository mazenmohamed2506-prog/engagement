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
          <!-- Front: Venue Image & Information -->
          <div class="flip-card__face flip-card__front">
            <div class="flip-card__arch">
              <img :src="venueImg" alt="Wedding venue" class="flip-card__image" />
            </div>

            <div class="flip-card__details">
              <span class="flip-card__tag">Wedding Reception</span>
              <h3 class="flip-card__venue-title">El Galaa Club</h3>
              <p class="flip-card__venue-location">Heliopolis · Cairo, Egypt</p>

              <div class="flip-card__cta-btn">
                <span class="flip-card__cta-icon-wrap">
                  <svg class="flip-card__cta-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"></path>
                    <circle cx="12" cy="10" r="3"></circle>
                  </svg>
                </span>
                <span class="flip-card__cta-label">Tap to See Location</span>
                <svg class="flip-card__cta-arrow" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
                  <polyline points="9 18 15 12 9 6"></polyline>
                </svg>
              </div>
            </div>
          </div>

          <!-- Back: QR Code -->
          <div class="flip-card__face flip-card__back">
            <div class="flip-card__qr-content">
              <span class="flip-card__back-badge">Google Maps</span>
              <p class="flip-card__qr-title">El Galaa Club</p>
              <div class="flip-card__qr-frame">
                <img :src="qrCodeDataUrl" alt="Venue QR code" class="flip-card__qr-image" />
              </div>
              <p class="flip-card__qr-subtitle">Scan QR code for directions</p>
              <a 
                :href="mapLocationUrl" 
                target="_blank" 
                rel="noopener noreferrer" 
                class="flip-card__qr-link"
                @click.stop
              >
                <svg viewBox="0 0 24 24" width="15" height="15" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                  <path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"></path>
                  <polyline points="15 3 21 3 21 9"></polyline>
                  <line x1="10" y1="14" x2="21" y2="3"></line>
                </svg>
                <span>Open in Google Maps</span>
              </a>
            </div>
            <div class="flip-card__back-hint">
              <svg viewBox="0 0 24 24" width="14" height="14" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M3 12a9 9 0 1 0 9-9 9.75 9.75 0 0 0-6.74 2.74L3 8"/>
                <path d="M3 3v5h5"/>
              </svg>
              <span>Tap to flip back</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import venueImg from '@/assets/images/hand1.jpg'
import qrCodeImg from '@/assets/images/qr-code.png'
import QRCode from 'qrcode'

const isFlipped = ref(false)
const mapLocationUrl = 'https://maps.app.goo.gl/Kmg8KSsX2PC4skTdA'
const qrCodeDataUrl = ref(qrCodeImg)

onMounted(async () => {
  try {
    qrCodeDataUrl.value = await QRCode.toDataURL(mapLocationUrl, {
      color: { dark: '#4a141aff', light: '#fbf8f5ff' },
      width: 400,
      margin: 2
    })
  } catch (e) {
    qrCodeDataUrl.value = qrCodeImg
  }
})
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
  max-width: 320px;
}

.flip-card__inner {
  position: relative;
  width: 100%;
  aspect-ratio: 3 / 4.35;
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
  border-radius: 16px;
  overflow: hidden;
  box-shadow: 0 10px 35px rgba(74, 20, 26, 0.14);
  border: 1px solid rgba(212, 175, 55, 0.25);
}

.flip-card__front {
  display: flex;
  flex-direction: column;
  background: var(--color-ivory);
}

.flip-card__arch {
  position: relative;
  flex: 1;
  min-height: 235px;
  border-radius: 150px 150px 0 0;
  overflow: hidden;
  margin: 10px 10px 0;
}

.flip-card__image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.flip-card__details {
  padding: 0.85rem 1rem 1rem;
  text-align: center;
  background: var(--color-ivory);
  display: flex;
  flex-direction: column;
  align-items: center;
}

.flip-card__tag {
  font-family: var(--font-sans);
  font-size: 0.58rem;
  font-weight: 700;
  letter-spacing: 0.22em;
  text-transform: uppercase;
  color: var(--color-gold-dark);
  margin-bottom: 0.2rem;
}

.flip-card__venue-title {
  font-family: var(--font-serif);
  font-size: 1.35rem;
  font-weight: 600;
  color: #4a141a;
  letter-spacing: 0.01em;
  margin: 0;
}

.flip-card__venue-location {
  font-family: var(--font-sans);
  font-size: 0.68rem;
  font-weight: 500;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  color: var(--color-navy-light);
  margin-top: 0.15rem;
  margin-bottom: 0.75rem;
  opacity: 0.85;
}

.flip-card__cta-btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 0.55rem;
  padding: 0.62rem 1.25rem;
  background: linear-gradient(135deg, #4a141a 0%, #6b1d26 100%);
  color: #ffffff;
  border: 1.5px solid rgba(212, 175, 55, 0.6);
  border-radius: 30px;
  box-shadow: 0 4px 15px rgba(74, 20, 26, 0.25), 0 0 0 2px rgba(212, 175, 55, 0.15);
  animation: ctaPulse 2.8s ease-in-out infinite;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.flip-card:hover .flip-card__cta-btn {
  transform: translateY(-2px) scale(1.02);
  box-shadow: 0 6px 20px rgba(74, 20, 26, 0.35), 0 0 0 3px rgba(212, 175, 55, 0.3);
  background: linear-gradient(135deg, #5c1821 0%, #7d222d 100%);
}

.flip-card__cta-icon-wrap {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 22px;
  height: 22px;
  border-radius: 50%;
  background: rgba(212, 175, 55, 0.25);
}

.flip-card__cta-icon {
  width: 13px;
  height: 13px;
  color: #ffd700;
  animation: pinBounce 1.8s ease-in-out infinite;
}

.flip-card__cta-label {
  font-family: var(--font-sans);
  font-size: 0.74rem;
  font-weight: 700;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: #ffffff;
  white-space: nowrap;
}

.flip-card__cta-arrow {
  width: 13px;
  height: 13px;
  color: var(--color-gold-light);
  transition: transform 0.3s ease;
}

.flip-card:hover .flip-card__cta-arrow {
  transform: translateX(3px);
}

@keyframes ctaPulse {
  0%, 100% {
    box-shadow: 0 4px 15px rgba(74, 20, 26, 0.25), 0 0 0 0 rgba(212, 175, 55, 0.4);
  }
  50% {
    box-shadow: 0 6px 22px rgba(74, 20, 26, 0.38), 0 0 0 6px rgba(212, 175, 55, 0);
  }
}

@keyframes pinBounce {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-2px); }
}

/* Back face */
.flip-card__back {
  transform: rotateY(180deg);
  background: linear-gradient(160deg, var(--color-warm-gray-dark), var(--color-ivory));
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  padding: 1.5rem 1rem 1rem;
}

.flip-card__back-badge {
  font-family: var(--font-sans);
  font-size: 0.58rem;
  font-weight: 700;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--color-gold-dark);
  margin-bottom: 0.2rem;
}

.flip-card__qr-content {
  text-align: center;
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.flip-card__qr-title {
  font-family: var(--font-serif);
  font-size: 1.15rem;
  font-weight: 600;
  color: var(--color-navy);
  margin-bottom: 1rem;
}

.flip-card__qr-frame {
  width: 155px;
  height: 155px;
  padding: 10px;
  background: var(--color-ivory);
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(74, 20, 26, 0.15);
  border: 1px solid rgba(196, 164, 155, 0.4);
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
  color: var(--color-navy-light);
  margin-top: 0.85rem;
  opacity: 0.8;
}

.flip-card__qr-link {
  display: inline-flex;
  align-items: center;
  gap: 0.45rem;
  margin-top: 0.85rem;
  font-family: var(--font-sans);
  font-size: 0.72rem;
  font-weight: 600;
  color: var(--color-gold-dark);
  text-decoration: none;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  padding: 0.5rem 1.1rem;
  border: 1.5px solid var(--color-gold-dark);
  border-radius: 20px;
  background: rgba(255, 255, 255, 0.6);
  transition: all 0.3s ease;
}

.flip-card__qr-link:hover {
  background: var(--color-gold-dark);
  color: var(--color-ivory);
  transform: translateY(-1px);
}

.flip-card__back-hint {
  display: inline-flex;
  align-items: center;
  gap: 0.35rem;
  font-family: var(--font-sans);
  font-size: 0.68rem;
  font-weight: 600;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--color-navy-light);
  padding: 0.4rem 0.8rem;
  border-radius: 12px;
  background: rgba(0, 0, 0, 0.04);
  opacity: 0.85;
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
  box-shadow: 0 2px 12px rgba(74, 20, 26, 0.05);
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
