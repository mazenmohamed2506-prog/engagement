<template>
  <section class="save-the-date" id="save-the-date">
    <div class="save-the-date__inner">
      <div class="save-the-date__overlay">
        <p class="save-the-date__save">Save</p>
        <p class="save-the-date__the">the</p>
        <p class="save-the-date__date-text">Date</p>
        <div class="save-the-date__line"></div>
        <p class="save-the-date__full-date">Thursday, July 30th</p>
        <p class="save-the-date__year">2026</p>
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
  background: var(--color-warm-gray-dark);
}

.save-the-date__inner {
  position: relative;
  width: 100%;
  aspect-ratio: 4 / 5;
  background-image: v-bind("`url('${seaWaves}')`");
  background-size: cover;
  background-position: center;
  border-radius: 16px;
  overflow: hidden;
  box-shadow: 0 10px 40px rgba(75, 61, 91, 0.15);
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
    rgba(255, 251, 247, 0.4) 0%,
    rgba(255, 251, 247, 0.2) 30%,
    rgba(255, 251, 247, 0.6) 80%,
    rgba(251, 248, 252, 0.9) 100%
  );
  text-align: center;
  padding: 2rem;
}

.save-the-date__save {
  font-family: var(--font-sans);
  font-size: 0.7rem;
  letter-spacing: 0.4em;
  color: var(--color-navy);
  margin-bottom: 0.5rem;
  text-transform: uppercase;
}

.save-the-date__the {
  font-family: var(--font-cursive);
  font-size: 2rem;
  color: var(--color-gold-dark);
  margin-bottom: -0.5rem;
}

.save-the-date__date-text {
  font-family: var(--font-serif);
  font-size: 3rem;
  font-weight: 500;
  color: var(--color-navy);
  letter-spacing: 0.1em;
  text-transform: uppercase;
}

.save-the-date__line {
  width: 60px;
  height: 1px;
  background: var(--color-gold);
  margin: 1.5rem auto;
}

.save-the-date__full-date {
  font-family: var(--font-serif);
  font-size: 0.9rem;
  font-style: italic;
  color: var(--color-navy);
  letter-spacing: 0.05em;
}

.save-the-date__year {
  font-family: var(--font-sans);
  font-size: 0.6rem;
  letter-spacing: 0.3em;
  color: var(--color-navy-light);
  margin-top: 0.5rem;
}
</style>
