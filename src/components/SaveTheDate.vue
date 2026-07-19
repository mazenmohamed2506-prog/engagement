<template>
  <section class="save-the-date" id="save-the-date">
    <div class="save-the-date__inner">
      <div class="save-the-date__arch">
        <img :src="seaWaves" alt="Ocean waves" class="save-the-date__image" />
        <div class="save-the-date__overlay">
          <p class="save-the-date__label">Save</p>
          <p class="save-the-date__the">the</p>
          <p class="save-the-date__date-text">Date</p>
          <div class="save-the-date__line"></div>
          <p class="save-the-date__full-date">Sunday, August 2nd</p>
          <p class="save-the-date__year">2026</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import seaWaves from '@/assets/images/sea-waves.png'
</script>

<style scoped>
.save-the-date {
  padding: 3rem 1.5rem;
  background: var(--color-warm-gray);
}

.save-the-date__inner {
  max-width: 320px;
  margin: 0 auto;
}

.save-the-date__arch {
  position: relative;
  width: 100%;
  aspect-ratio: 3 / 4;
  border-radius: 200px 200px 0 0;
  overflow: hidden;
  box-shadow: 0 12px 40px rgba(26, 39, 68, 0.15);
}

.save-the-date__image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.save-the-date__overlay {
  position: absolute;
  inset: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: linear-gradient(
    to bottom,
    rgba(26, 39, 68, 0.25) 0%,
    rgba(26, 39, 68, 0.5) 100%
  );
  text-align: center;
  padding: 2rem;
}

.save-the-date__label {
  font-family: var(--font-sans);
  font-size: 0.7rem;
  letter-spacing: 0.45em;
  text-transform: uppercase;
  color: var(--color-ivory);
}

.save-the-date__the {
  font-family: var(--font-cursive);
  font-size: 2rem;
  color: var(--color-gold-light);
  margin: 0.25rem 0;
}

.save-the-date__date-text {
  font-family: var(--font-serif);
  font-size: 3rem;
  font-weight: 600;
  color: #fff;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  line-height: 1;
}

.save-the-date__line {
  width: 50px;
  height: 1px;
  background: var(--color-gold);
  margin: 1.25rem auto;
}

.save-the-date__full-date {
  font-family: var(--font-serif);
  font-size: 0.95rem;
  color: var(--color-ivory);
  font-style: italic;
}

.save-the-date__year {
  font-family: var(--font-sans);
  font-size: 0.7rem;
  letter-spacing: 0.4em;
  color: var(--color-gold-light);
  margin-top: 0.5rem;
}
</style>
