<template>
  <section ref="root" class="hero" :class="{ 'is-visible': visible }">
    <div class="hero__backdrop" aria-hidden="true"></div>
    <div class="hero__grid-bg" aria-hidden="true"></div>

    <span class="marker marker--tl" aria-hidden="true">+</span>
    <span class="marker marker--tr" aria-hidden="true">+</span>
    <span class="marker marker--bl" aria-hidden="true">+</span>
    <span class="marker marker--br" aria-hidden="true">+</span>

    <header class="hero__head">
      <span class="hero__label">00 — Студия</span>
      <h1 class="hero__title">Kadr Dev</h1>
      <span class="hero__meta">Moscow · 2026</span>
    </header>

    <div class="hero__stage">
      <span class="hero__kicker">
        <span class="hero__kicker-num">01</span>
        Заказная разработка
      </span>

      <h2 class="hero__headline">
        Сайты, CRM
        и телеграм-боты
        <span class="hero__accent">под задачу бизнеса</span>
      </h2>

      <p class="hero__desc">
        Vue, Node, Python. Работаем напрямую с командой — без менеджеров
        и агентств. От прототипа в Figma до продакшена.
      </p>

      <div class="hero__actions">
        <a href="#contact" class="btn btn--solid">
          <span>Обсудить проект</span>
          <span class="btn__arrow">→</span>
        </a>
      </div>

      <div class="hero__example">
        <span class="hero__example-label">Пример работы</span>

        <div class="example">
          <span class="example__name">Этот сайт — один из наших проектов</span>
          <span class="example__meta">Vue 3 · SCSS · ECharts · 2026</span>
          <span class="example__arrow">↓</span>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue'

/**
 * Hero — вводная секция.
 * Единственный CTA — «Обсудить проект».
 * Ниже — строка примера: весь сайт целиком является примером работы.
 */

const root = ref(null)
const visible = ref(false)
let observer = null

onMounted(() => {
  if (typeof IntersectionObserver === 'undefined') {
    visible.value = true
    return
  }

  observer = new IntersectionObserver(
    async (entries) => {
      for (const entry of entries) {
        if (entry.isIntersecting && entry.intersectionRatio >= 0.35) {
          if (visible.value) return
          await nextTick()
          visible.value = true
        } else if (!entry.isIntersecting) {
          visible.value = false
        }
      }
    },
    { threshold: [0, 0.35, 0.6] }
  )

  if (root.value) observer.observe(root.value)
})

onBeforeUnmount(() => {
  if (observer && root.value) observer.unobserve(root.value)
  observer = null
})
</script>

<style scoped lang="scss">
@use "../styles/variables" as *;

/* ==========================================================================
   ПЕРЕМЕННЫЕ
   ========================================================================== */

$text:        #f4ecdf;
$paper:       #ede0c8;
$muted:       rgba(244, 236, 223, 0.6);
$muted-2:     rgba(244, 236, 223, 0.35);

$hairline:    rgba(200, 170, 135, 0.16);
$faint:       rgba(200, 170, 135, 0.10);

$accent:      #c8874a;
$espresso:    #100a06;

$serif: Georgia, "Times New Roman", serif;
$mono: "IBM Plex Mono", "JetBrains Mono", ui-monospace,
       SFMono-Regular, Menlo, Consolas, monospace;

$padding-x:      5vw;
$padding-top:    18px;
$padding-bottom: 14px;

$ease-soft: cubic-bezier(0.25, 0.46, 0.45, 0.94);

/* ==========================================================================
   KEYFRAMES
   ========================================================================== */

@keyframes fade-in {
  from { opacity: 0; }
  to   { opacity: 1; }
}

@keyframes fade-down {
  from { opacity: 0; transform: translateY(-8px); }
  to   { opacity: 1; transform: translateY(0);    }
}

@keyframes fade-up {
  from { opacity: 0; transform: translateY(12px); }
  to   { opacity: 1; transform: translateY(0);    }
}

/* ==========================================================================
   БЛОК
   ========================================================================== */

.hero {
  position: relative;

  display: flex;
  flex-direction: column;

  width: $size-full;
  height: 100%;
  min-height: 0;

  padding: $padding-top $padding-x $padding-bottom;

  color: $text;

  background-color: $espresso;

  overflow: hidden;

  &__backdrop {
    position: absolute;
    inset: 0;

    background:
      radial-gradient(
        70% 60% at 15% 20%,
        rgba(200, 135, 74, 0.20) 0%,
        rgba(200, 135, 74, 0.0) 60%
      ),
      radial-gradient(
        70% 60% at 85% 85%,
        rgba(120, 80, 50, 0.22) 0%,
        rgba(120, 80, 50, 0.0) 60%
      ),
      linear-gradient(
        to bottom,
        rgba(23, 16, 12, 0.95) 0%,
        rgba(23, 16, 12, 0.55) 55%,
        rgba(23, 16, 12, 0.0) 100%
      );

    pointer-events: none;
    z-index: 0;

    opacity: 0;
    .hero.is-visible & {
      animation: fade-in 1.4s $ease-soft 0.05s both;
    }
  }

  &__grid-bg {
    position: absolute;
    inset: 0;

    background-image:
      linear-gradient(to right, $faint 1px, transparent 1px),
      linear-gradient(to bottom, $faint 1px, transparent 1px);
    background-size: 72px 72px;
    background-position: $padding-x $padding-top;

    mask-image: radial-gradient(
      120% 90% at 50% 50%,
      #000 40%,
      transparent 100%
    );
    -webkit-mask-image: radial-gradient(
      120% 90% at 50% 50%,
      #000 40%,
      transparent 100%
    );

    pointer-events: none;
    z-index: 0;

    opacity: 0;
    .hero.is-visible & {
      animation: fade-in 1.6s $ease-soft 0.15s both;
    }
  }

  &__head {
    position: relative;
    z-index: 20;

    display: grid;
    grid-template-columns: 1fr auto;
    align-items: end;
    gap: 12px;

    flex: none;
    padding-bottom: 12px;

    border-bottom: 1px solid $hairline;

    > * { opacity: 0; }

    .hero.is-visible & > * {
      animation: fade-down 0.8s $ease-soft both;
    }

    .hero.is-visible & > *:nth-child(1) { animation-delay: 0.15s; }
    .hero.is-visible & > *:nth-child(2) { animation-delay: 0.25s; }
    .hero.is-visible & > *:nth-child(3) { animation-delay: 0.35s; }
  }

  &__label,
  &__meta,
  &__kicker,
  &__example-label {
    font-family: $mono;
    letter-spacing: 0.22em;
    text-transform: uppercase;
  }

  &__label {
    font-size: 0.6875rem;
    font-weight: 600;
    color: $muted;
  }

  &__title {
    grid-column: 1 / 2;
    margin: 0;

    font-family: $serif;
    font-size: clamp(1.75rem, 3vw, 2.5rem);
    font-weight: 400;
    line-height: 1;
    letter-spacing: -0.025em;

    color: $paper;
  }

  &__meta {
    grid-column: 2 / 3;
    grid-row: 1 / 3;
    align-self: start;

    font-size: 0.625rem;
    color: $muted;
  }

  &__stage {
    position: relative;
    z-index: 1;

    flex: 1 1 auto;
    min-height: 0;

    display: flex;
    flex-direction: column;
    justify-content: center;
    gap: 18px;

    padding: 18px 0 12px;
  }

  &__kicker {
    display: inline-flex;
    align-items: center;
    gap: 12px;

    font-size: 0.625rem;
    font-weight: 600;
    color: $muted;

    opacity: 0;
    .hero.is-visible & {
      animation: fade-up 0.8s $ease-soft 0.45s both;
    }
  }

  &__kicker-num {
    font-weight: 700;
    color: $accent;
  }

  &__kicker::after {
    content: "";
    width: 36px;
    height: 1px;
    background: $hairline;
  }

  &__headline {
    margin: 0;

    font-family: $serif;
    font-size: clamp(1.875rem, 3.8vw, 3.25rem);
    font-weight: 400;
    line-height: 1.05;
    letter-spacing: -0.025em;

    color: $paper;

    opacity: 0;
    .hero.is-visible & {
      animation: fade-up 1s $ease-soft 0.55s both;
    }
  }

  &__accent {
    display: block;
    color: $accent;
    font-weight: 400;
  }

  &__desc {
    max-width: 52ch;
    margin: 0;

    font-family: $serif;
    font-size: 0.9375rem;
    line-height: 1.5;
    color: rgba(244, 236, 223, 0.72);

    opacity: 0;
    .hero.is-visible & {
      animation: fade-up 0.9s $ease-soft 0.65s both;
    }
  }

  &__actions {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;

    margin-top: 2px;

    opacity: 0;
    .hero.is-visible & {
      animation: fade-up 0.9s $ease-soft 0.75s both;
    }
  }

  &__example {
    display: grid;
    grid-template-columns: 140px 1fr;
    align-items: center;
    gap: 20px;

    margin-top: 6px;
    padding-top: 14px;

    border-top: 1px solid $hairline;

    opacity: 0;
    .hero.is-visible & {
      animation: fade-up 0.9s $ease-soft 0.9s both;
    }
  }

  &__example-label {
    font-size: 0.5625rem;
    color: $muted-2;
  }
}

/* ==========================================================================
   ТЕХНО-МАРКЕРЫ
   ========================================================================== */

.marker {
  position: absolute;

  font-family: $mono;
  font-size: 12px;
  line-height: 1;
  color: rgba(242, 233, 220, 0.3);

  pointer-events: none;
  z-index: 15;

  opacity: 0;
  .hero.is-visible & {
    animation: fade-in 0.8s $ease-soft 1s both;
  }

  &--tl { left:  $padding-x; top:    $padding-top; }
  &--tr { right: $padding-x; top:    $padding-top; }
  &--bl { left:  $padding-x; bottom: $padding-bottom; }
  &--br { right: $padding-x; bottom: $padding-bottom; }
}

/* ==========================================================================
   ПРИМЕР РАБОТЫ
   ========================================================================== */

.example {
  display: grid;
  grid-template-columns: 1fr auto auto;
  align-items: baseline;
  gap: 24px;

  &__name {
    font-family: $serif;
    font-size: 1.0625rem;
    font-weight: 400;
    letter-spacing: -0.01em;
    color: $paper;
  }

  &__meta {
    font-family: $mono;
    font-size: 0.625rem;
    letter-spacing: 0.16em;
    text-transform: uppercase;
    color: $muted-2;
  }

  &__arrow {
    font-family: $mono;
    font-size: 0.9375rem;
    color: $accent;

    animation: pulse 2s $ease-soft infinite;
  }
}

@keyframes pulse {
  0%, 100% { transform: translateY(0);   opacity: 0.85; }
  50%      { transform: translateY(4px); opacity: 1;    }
}

/* ==========================================================================
   КНОПКА
   ========================================================================== */

.btn {
  display: inline-flex;
  align-items: center;
  justify-content: space-between;
  gap: 18px;

  padding: 11px 20px;

  font-family: $mono;
  font-size: 0.6875rem;
  font-weight: 600;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  text-decoration: none;

  border: 1px solid transparent;
  border-radius: 2px;

  cursor: pointer;
  transition:
    background-color 0.3s $ease-soft,
    color            0.3s $ease-soft,
    border-color     0.3s $ease-soft,
    transform        0.3s $ease-soft;

  &__arrow {
    display: inline-block;
    font-size: 0.875rem;
    letter-spacing: 0;

    transition: transform 0.3s $ease-soft;
  }

  &:hover &__arrow { transform: translateX(4px); }

  &--solid {
    background-color: $accent;
    color: #100a06;
    border-color: $accent;

    &:hover {
      background-color: #d99b5e;
      border-color: #d99b5e;
      transform: translateY(-1px);
    }
  }
}

/* ==========================================================================
   АДАПТИВ
   ========================================================================== */

@media (max-width: 900px) {
  .hero {
    height: auto;
    min-height: 0;
    padding: 20px 5vw 16px;
  }

  .hero__stage {
    gap: 16px;
    padding: 18px 0 8px;
  }

  .hero__headline {
    font-size: clamp(1.625rem, 7vw, 2.25rem);
  }

  .hero__desc { font-size: 0.875rem; }

  .hero__example {
    grid-template-columns: 1fr;
    gap: 8px;
  }

  .example {
    grid-template-columns: 1fr auto;
    gap: 10px;

    &__meta {
      grid-column: 1 / 2;
      grid-row: 2 / 3;
    }

    &__arrow {
      grid-row: 1 / 3;
      align-self: center;
    }
  }

  .hero__actions {
    flex-direction: column;
    align-items: stretch;
  }

  .btn { width: 100%; }
}
</style>