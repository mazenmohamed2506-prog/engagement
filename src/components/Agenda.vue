<template>
  <section class="agenda" id="agenda">
    <div class="agenda__inner">
      <h2 class="agenda__heading">Order of the Day</h2>

      <svg class="agenda__divider" viewBox="0 0 200 20" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M0 10 Q25 0 50 10 Q75 20 100 10 Q125 0 150 10 Q175 20 200 10" stroke="currentColor" stroke-width="1" fill="none" opacity="0.5"/>
        <circle cx="100" cy="10" r="3" fill="currentColor" opacity="0.6"/>
        <line x1="60" y1="10" x2="85" y2="10" stroke="currentColor" stroke-width="0.5" opacity="0.4"/>
        <line x1="115" y1="10" x2="140" y2="10" stroke="currentColor" stroke-width="0.5" opacity="0.4"/>
      </svg>

      <div class="agenda__timeline">
        <div
          v-for="(event, index) in events"
          :key="index"
          ref="cardRefs"
          class="agenda__card"
          :class="{ 'agenda__card--visible': visibleCards[index] }"
        >
          <div class="agenda__card-icon">
            <component :is="event.icon" />
          </div>
          <div class="agenda__card-content">
            <span class="agenda__card-time">{{ event.time }}</span>
            <h3 class="agenda__card-title">{{ event.title }}</h3>
            <p class="agenda__card-desc">{{ event.description }}</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted, h } from 'vue'

// Simple SVG icon components
const GlassIcon = {
  render: () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '1.5', 'stroke-linecap': 'round', 'stroke-linejoin': 'round' }, [
    h('path', { d: 'M8 22h8' }),
    h('path', { d: 'M12 11v11' }),
    h('path', { d: 'M19.5 2L17 11H7L4.5 2' }),
  ])
}

const CameraIcon = {
  render: () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '1.5', 'stroke-linecap': 'round', 'stroke-linejoin': 'round' }, [
    h('path', { d: 'M23 19a2 2 0 0 1-2 2H3a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h4l2-3h6l2 3h4a2 2 0 0 1 2 2z' }),
    h('circle', { cx: '12', cy: '13', r: '4' }),
  ])
}

const HeartIcon = {
  render: () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '1.5', 'stroke-linecap': 'round', 'stroke-linejoin': 'round' }, [
    h('path', { d: 'M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z' }),
  ])
}

const UtensilsIcon = {
  render: () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '1.5', 'stroke-linecap': 'round', 'stroke-linejoin': 'round' }, [
    h('path', { d: 'M3 2v7c0 1.1.9 2 2 2h4a2 2 0 0 0 2-2V2' }),
    h('path', { d: 'M7 2v20' }),
    h('path', { d: 'M21 15V2v0a5 5 0 0 0-5 5v6c0 1.1.9 2 2 2h3zm0 0v7' }),
  ])
}

const MusicIcon = {
  render: () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '1.5', 'stroke-linecap': 'round', 'stroke-linejoin': 'round' }, [
    h('path', { d: 'M9 18V5l12-2v13' }),
    h('circle', { cx: '6', cy: '18', r: '3' }),
    h('circle', { cx: '18', cy: '16', r: '3' }),
  ])
}

const SparkleIcon = {
  render: () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '1.5', 'stroke-linecap': 'round', 'stroke-linejoin': 'round' }, [
    h('polygon', { points: '12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2' }),
  ])
}

const events = [
  {
    time: '7:00 PM',
    title: 'Guest Arrival',
    description: 'Join us as we gather to celebrate',
    icon: GlassIcon,
  },
  {
    time: '7:30 PM',
    title: 'Engagement Ceremony',
    description: 'The ring exchange ceremony begins',
    icon: HeartIcon,
  },
  {
    time: '8:00 PM',
    title: 'Photo Session',
    description: 'Capture beautiful memories with us',
    icon: CameraIcon,
  },
  {
    time: '8:30 PM',
    title: 'Dinner',
    description: 'A curated dining experience awaits',
    icon: UtensilsIcon,
  },
  {
    time: '9:15 PM',
    title: 'Celebration & Dancing',
    description: 'Celebrate the night with music and joy',
    icon: MusicIcon,
  }
]

const cardRefs = ref([])
const visibleCards = ref(events.map(() => false))
let observers = []

onMounted(() => {
  // Wait a tick for refs to populate
  setTimeout(() => {
    if (!cardRefs.value) return
    const cards = Array.isArray(cardRefs.value) ? cardRefs.value : [cardRefs.value]

    cards.forEach((card, index) => {
      if (!card) return
      const observer = new IntersectionObserver(
        (entries) => {
          entries.forEach((entry) => {
            if (entry.isIntersecting) {
              visibleCards.value[index] = true
              observer.unobserve(entry.target)
            }
          })
        },
        { threshold: 0.15 }
      )
      observer.observe(card)
      observers.push(observer)
    })
  }, 100)
})

onUnmounted(() => {
  observers.forEach((obs) => obs.disconnect())
  observers = []
})
</script>

<style scoped>
.agenda {
  padding: 4rem 1.5rem;
  background: var(--color-warm-gray);
}

.agenda__inner {
  max-width: 400px;
  margin: 0 auto;
}

.agenda__heading {
  font-family: var(--font-serif);
  font-size: 1.75rem;
  font-weight: 500;
  color: var(--color-navy);
  text-align: center;
  margin-bottom: 0.75rem;
}

.agenda__divider {
  display: block;
  width: 140px;
  height: 20px;
  margin: 0 auto 2.5rem;
  color: var(--color-gold);
}

.agenda__timeline {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.agenda__card {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
  padding: 1.25rem;
  background: var(--color-ivory);
  border-radius: 8px;
  box-shadow: 0 2px 12px rgba(75, 61, 91, 0.05);
  border: 1px solid var(--color-warm-gray-dark);
  opacity: 0;
  transform: translateY(30px);
  transition: opacity 0.6s ease, transform 0.6s ease;
}

.agenda__card--visible {
  opacity: 1;
  transform: translateY(0);
}

.agenda__card-icon {
  flex-shrink: 0;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--color-ivory-dark);
  color: var(--color-gold-dark);
  border-radius: 50%;
  padding: 8px;
}

.agenda__card-icon svg {
  width: 20px;
  height: 20px;
}

.agenda__card-content {
  flex: 1;
}

.agenda__card-time {
  font-family: var(--font-sans);
  font-size: 0.65rem;
  font-weight: 600;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--color-gold-dark);
}

.agenda__card-title {
  font-family: var(--font-serif);
  font-size: 1.1rem;
  font-weight: 500;
  color: var(--color-navy);
  margin: 0.25rem 0;
}

.agenda__card-desc {
  font-family: var(--font-sans);
  font-size: 0.75rem;
  color: var(--color-navy-light);
  opacity: 0.7;
  line-height: 1.5;
}
</style>
