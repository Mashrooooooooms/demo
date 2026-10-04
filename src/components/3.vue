<template>
  <section ref="root" class="collage" :class="{ 'is-visible': visible }">
    <!-- Фон: тонкая техническая сетка + тёплое свечение снизу -->
    <div class="collage__backdrop" aria-hidden="true"></div>
    <div class="collage__grid" aria-hidden="true"></div>

    <header class="collage__head">
      <span class="collage__label">02 — Коллаж</span>
      <h2 class="collage__title">Формы</h2>
      <span class="collage__meta">06 · MMXXVI</span>
    </header>

    <div class="collage__stage">
      <!-- Техно-маркеры по углам -->
      <span class="marker marker--tl" aria-hidden="true">+</span>
      <span class="marker marker--tr" aria-hidden="true">+</span>
      <span class="marker marker--bl" aria-hidden="true">+</span>
      <span class="marker marker--br" aria-hidden="true">+</span>

      <!-- ============================================================
           СНОСКИ: объясняют формы, пропорции и логику коллажа
           ============================================================ -->

      <!-- Сетка + маркеры -->
      <div class="anno anno--grid">
        <span class="anno__dot"></span>
        <span class="anno__line"></span>
        <span class="anno__text">
          <b>Каркас</b>
          <em>Сетка 72 px + маркеры по углам — техническая рамка листа.</em>
        </span>
      </div>

      <!-- Портретный кадр -->
      <div class="anno anno--portrait">
        <span class="anno__dot"></span>
        <span class="anno__line"></span>
        <span class="anno__text">
          <b>Форма 3:4</b>
          <em>Портретный кадр — задаёт вертикальный ритм слева.</em>
        </span>
      </div>

      <!-- Широкий кадр -->
      <div class="anno anno--landscape">
        <span class="anno__dot"></span>
        <span class="anno__line"></span>
        <span class="anno__text">
          <b>Форма 4:3</b>
          <em>Широкий кадр — разряжает плотность и даёт воздух.</em>
        </span>
      </div>

      <!-- Квадрат -->
      <div class="anno anno--square">
        <span class="anno__dot"></span>
        <span class="anno__line"></span>
        <span class="anno__text">
          <b>Форма 1:1</b>
          <em>Квадрат — плотный центр, точка опоры взгляда.</em>
        </span>
      </div>

      <!-- Вертикаль -->
      <div class="anno anno--tall">
        <span class="anno__dot"></span>
        <span class="anno__line"></span>
        <span class="anno__text">
          <b>Форма 2:5</b>
          <em>Узкая вертикаль — акцент и контраст к широким форматам.</em>
        </span>
      </div>

      <!-- Наклон -->
      <div class="anno anno--tilt">
        <span class="anno__dot"></span>
        <span class="anno__line"></span>
        <span class="anno__text">
          <b>Наклон ±2–6°</b>
          <em>Лёгкий поворот каждой плитки — ручная сборка, без линейки.</em>
        </span>
      </div>

      <!-- Редакционный блок -->
      <div class="anno anno--note">
        <span class="anno__dot"></span>
        <span class="anno__line"></span>
        <span class="anno__text">
          <b>Анкер</b>
          <em>Редакционный блок по центру — смысловая точка композиции.</em>
        </span>
      </div>

      <!-- 01 — вертикальный кадр слева -->
      <figure class="tile tile--portrait tile--1">
        <img src="/les.jpg" alt="">
        <figcaption class="tile__cap">
          <span class="tile__idx">01</span>
          <span class="tile__label">Тень</span>
        </figcaption>
      </figure>

      <!-- 02 — широкий горизонтальный сверху -->
      <figure class="tile tile--landscape tile--2">
        <img src="/portret.jpg" alt="">
        <figcaption class="tile__cap">
          <span class="tile__idx">02</span>
          <span class="tile__label">Свет · портрет</span>
        </figcaption>
      </figure>

      <!-- 03 — квадрат -->
      <figure class="tile tile--square tile--3">
        <img src="/transport.png" alt="">
        <figcaption class="tile__cap">
          <span class="tile__idx">03</span>
          <span class="tile__label">Город · ритм</span>
        </figcaption>
      </figure>

      <!-- 04 — узкая вертикаль -->
      <figure class="tile tile--tall tile--4">
        <img src="/i.webp" alt="">
        <figcaption class="tile__cap">
          <span class="tile__idx">04</span>
          <span class="tile__label">Кадр</span>
        </figcaption>
      </figure>

      <!-- 05 — горизонтальный внизу -->
      <figure class="tile tile--landscape tile--5">
        <img src="/vert.webp" alt="">
        <figcaption class="tile__cap">
          <span class="tile__idx">05</span>
          <span class="tile__label">Фрагмент</span>
        </figcaption>
      </figure>

      <!-- 06 — квадрат, поверх -->
      <figure class="tile tile--square tile--6">
        <img src="/komposition.jpg" alt="">
        <figcaption class="tile__cap">
          <span class="tile__idx">06</span>
          <span class="tile__label">Композиция</span>
        </figcaption>
      </figure>

      <!-- Журнальный редакционный блок -->
      <div class="note">
        <span class="note__kicker">Editorial · Issue 01</span>
        <p class="note__text">
          Шесть кадров одной серии. Свет, город, фрагменты —
          собрано в один лист без правил.
        </p>
        <span class="note__sig">— Лофт «Кадр»</span>
      </div>
    </div>

    <!-- Подпись в правом нижнем углу -->
    <div class="collage__sign">
      <span class="collage__sign-name">Лофт «Кадр»</span>
      <span class="collage__sign-line">Коллаж · 2026</span>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue'

/**
 * 3.vue — третий блок.
 * Журнальный коллаж: шесть плиток разной геометрии.
 * Форма, размеры, позиции, повороты — без изменений.
 * Фотографии сдвинуты по кругу: каждая перешла на следующую плитку.
 *
 * Раскладка плиток:
 *   01 — portrait  /les.jpg
 *   02 — landscape /portret.jpg
 *   03 — square    /transport.png
 *   04 — tall      /i.webp
 *   05 — landscape /vert.webp
 *   06 — square    /komposition.jpg
 *
 * Сноски объясняют формы (пропорции), наклон, каркас и роль
 * редакционного блока. На мобилке сноски скрываются,
 * а сцена (плитки + анкер) пропорционально уменьшается через zoom.
 *
 * Палитра — кофейная: эспрессо-фон, тёплая бумага, карамельный акцент.
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
   ПЕРЕМЕННЫЕ — КОФЕЙНАЯ ПАЛИТРА
   ========================================================================== */

// --- Цвета ---
$text:        #f2e9dc;
$muted:       rgba(242, 233, 220, 0.55);
$faint:       rgba(200, 170, 135, 0.12);

$paper:       #e6d7bf;
$paper-deep:  #d3bf9d;

$ink:         #2a1d14;
$ink-soft:    rgba(42, 29, 20, 0.62);

$accent:      #c8874a;
$accent-deep: #8a5a2c;

$espresso:    #17100c;
$espresso-2:  #241811;

// --- Отступы блока ---
$padding-x:      5vw;
$padding-top:    3vh;
$padding-bottom: 7vh;

// --- Шапка ---
$label-size:      0.6875rem;
$label-spacing:   0.28em;
$label-weight:    600;

$title-size:    2.5rem;
$title-weight:  300;
$title-spacing: -0.02em;

// --- Техно-шрифт ---
$mono: "IBM Plex Mono", "JetBrains Mono", ui-monospace,
       SFMono-Regular, Menlo, Consolas, monospace;

// --- Ease ---
$ease-soft: cubic-bezier(0.25, 0.46, 0.45, 0.94);

/* ==========================================================================
   KEYFRAMES
   ========================================================================== */

@keyframes fade-in {
  from { opacity: 0; }
  to   { opacity: 1; }
}

@keyframes fade-down {
  from { opacity: 0; transform: translateY(-10px); }
  to   { opacity: 1; transform: translateY(0);     }
}

@keyframes tile-in {
  from { opacity: 0; transform: rotate(var(--rot, 0deg)) translateY(28px) scale(0.94); }
  to   { opacity: 1; transform: rotate(var(--rot, 0deg)) translateY(0)    scale(1);    }
}

@keyframes note-in {
  from { opacity: 0; transform: translate(-50%, -50%) rotate(-1.5deg) scale(0.96); }
  to   { opacity: 1; transform: translate(-50%, -50%) rotate(-1.5deg) scale(1);    }
}

@keyframes anno-in {
  from { opacity: 0; transform: translateY(-4px); }
  to   { opacity: 1; transform: translateY(0);    }
}

/* ==========================================================================
   БЛОК
   ========================================================================== */

.collage {
  position: relative;

  display: flex;
  flex-direction: column;

  width: $size-full;
  height: $size-full;

  padding: $padding-top $padding-x $padding-bottom;

  color: $text;

  overflow: hidden;

  // --- Нижнее тёплое свечение ---
  &__backdrop {
    position: absolute;
    inset: $size-zero;

    background:
      radial-gradient(
        100% 70% at 20% 100%,
        rgba(200, 135, 74, 0.22) 0%,
        rgba(200, 135, 74, 0.0) 55%
      ),
      radial-gradient(
        80% 60% at 85% 0%,
        rgba(120, 80, 50, 0.22) 0%,
        rgba(120, 80, 50, 0.0) 60%
      ),
      linear-gradient(
        to top,
        rgba(23, 16, 12, 0.95) 0%,
        rgba(23, 16, 12, 0.45) 55%,
        rgba(23, 16, 12, 0.0) 100%
      );

    pointer-events: none;
    z-index: $size-zero;

    opacity: 0;
    .collage.is-visible & {
      animation: fade-in 1.4s $ease-soft 0.05s both;
    }
  }

  // --- Тёплая сетка ---
  &__grid {
    position: absolute;
    inset: $size-zero;

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
    z-index: $size-zero;

    opacity: 0;
    .collage.is-visible & {
      animation: fade-in 1.6s $ease-soft 0.15s both;
    }
  }

  // --- Шапка ---
  &__head {
    position: relative;
    z-index: 20;

    display: grid;
    grid-template-columns: 1fr auto;
    align-items: end;

    gap: $space-sm;

    flex: $flex-none;
    margin-bottom: 2vh;

    > * {
      opacity: 0;
    }

    .collage.is-visible & > * {
      animation: fade-down 0.9s $ease-soft both;
    }

    .collage.is-visible & > *:nth-child(1) { animation-delay: 0.15s; }
    .collage.is-visible & > *:nth-child(2) { animation-delay: 0.28s; }
    .collage.is-visible & > *:nth-child(3) { animation-delay: 0.40s; }
  }

  &__label,
  &__sign-name,
  &__sign-line {
    font-size: $label-size;
    font-weight: $label-weight;
    letter-spacing: $label-spacing;
    text-transform: uppercase;
  }

  &__label {
    color: $muted;
  }

  &__title {
    font-size: $title-size;
    font-weight: $title-weight;
    letter-spacing: $title-spacing;

    grid-column: 1 / 2;
  }

  &__meta {
    grid-column: 2 / 3;
    grid-row: 1 / 3;
    align-self: start;

    font-family: $mono;
    font-size: 0.625rem;
    letter-spacing: 0.18em;
    color: $muted;
  }

  &__stage {
    position: relative;
    z-index: 1;

    flex: $flex-grow;
    min-height: $size-zero;
  }

  &__sign {
    position: absolute;
    right:  $padding-x;
    bottom: $padding-bottom;

    display: flex;
    flex-direction: column;
    align-items: flex-end;
    gap: 2px;

    text-align: right;

    z-index: 30;
    pointer-events: none;

    opacity: 0;
    .collage.is-visible & {
      animation: fade-in 1s $ease-soft 1.5s both;
    }

    &-name { color: $text; }
    &-line { color: $muted; }
  }
}

/* ==========================================================================
   ТЕХНО-МАРКЕРЫ
   ========================================================================== */

.marker {
  position: absolute;

  font-family: $mono;
  font-size: 14px;
  line-height: 1;
  color: rgba(242, 233, 220, 0.32);

  pointer-events: none;
  z-index: 15;

  opacity: 0;
  .collage.is-visible & {
    animation: fade-in 0.9s $ease-soft 1.15s both;
  }

  &--tl { left:  0; top:    0; }
  &--tr { right: 0; top:    0; }
  &--bl { left:  0; bottom: 0; }
  &--br { right: 0; bottom: 0; }
}

/* ==========================================================================
   ПЛИТКА
   ========================================================================== */

.tile {
  position: absolute;

  margin: $size-zero;

  background-color: $paper;

  overflow: hidden;

  opacity: 0;

  box-shadow:
    0 22px 50px rgba(15, 8, 5, 0.55),
    0 0 0 1px rgba(200, 170, 135, 0.10);

  transform: rotate(var(--rot, 0deg));

  img {
    display: block;
    width: $size-full;
    height: $size-full;

    object-fit: cover;

    filter: sepia(0.14) saturate(0.88) contrast(1.03) brightness(0.96);
  }

  &__cap {
    position: absolute;
    left: 10px;
    right: 10px;
    bottom: 8px;

    display: flex;
    align-items: baseline;
    gap: 8px;

    font-family: $mono;
    font-size: 0.5625rem;
    letter-spacing: 0.14em;
    text-transform: uppercase;

    color: $ink;

    &::before {
      content: "";
      position: absolute;
      left: -10px;
      right: -10px;
      bottom: -8px;
      top: -6px;

      background: linear-gradient(
        to top,
        rgba(230, 215, 191, 0.92) 0%,
        rgba(230, 215, 191, 0.0) 100%
      );

      pointer-events: none;
      z-index: -1;
    }
  }

  &__idx {
    font-weight: 700;
    color: $ink;
  }

  &__label {
    color: $ink-soft;
  }

  &--portrait  { width: 26%; aspect-ratio: 3 / 4;  }
  &--landscape { width: 34%; aspect-ratio: 4 / 3;  }
  &--square    { width: 20%; aspect-ratio: 1 / 1;  }
  &--tall      { width: 14%; aspect-ratio: 2 / 5;  }

  &--1 {
    left: 3%;
    top: 8%;

    --rot: -3deg;
    z-index: 2;
  }

  &--2 {
    left: 25%;
    top: 0%;

    --rot:  2deg;
    z-index: 4;
  }

  &--3 {
    right: 24%;
    top: 12%;

    --rot: -6deg;
    z-index: 5;
  }

  &--4 {
    right: 6%;
    top: 4%;

    --rot:  4deg;
    z-index: 3;
  }

  &--5 {
    left: 12%;
    bottom: 8%;

    --rot:  3deg;
    z-index: 3;
  }

  &--6 {
    right: 28%;
    bottom: 6%;

    --rot: -2deg;
    z-index: 6;
  }

  .collage.is-visible & {
    animation: tile-in 1.05s $ease-soft both;
  }

  .collage.is-visible &--1 { animation-delay: 0.50s; }
  .collage.is-visible &--2 { animation-delay: 0.63s; }
  .collage.is-visible &--3 { animation-delay: 0.76s; }
  .collage.is-visible &--4 { animation-delay: 0.89s; }
  .collage.is-visible &--5 { animation-delay: 1.02s; }
  .collage.is-visible &--6 { animation-delay: 1.15s; }
}

/* ==========================================================================
   ЖУРНАЛЬНЫЙ ТЕКСТОВЫЙ БЛОК
   ========================================================================== */

.note {
  position: absolute;

  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%) rotate(-1.5deg);

  width: 32%;
  max-width: 360px;

  padding: 16px 20px 14px;

  color: $ink;
  background-color: rgba(230, 215, 191, 0.94);

  border-left: 3px solid $accent;
  box-shadow: 0 18px 44px rgba(15, 8, 5, 0.5);

  z-index: 7;

  opacity: 0;
  .collage.is-visible & {
    animation: note-in 1.1s $ease-soft 1.3s both;
  }

  &__kicker {
    display: block;

    margin-bottom: 8px;

    font-family: $mono;
    font-size: 0.5625rem;
    font-weight: 700;
    letter-spacing: 0.32em;
    text-transform: uppercase;
    color: $ink-soft;
  }

  &__text {
    margin: 0 0 8px;

    font-family: Georgia, "Times New Roman", serif;
    font-size: 0.875rem;
    line-height: 1.45;
    letter-spacing: 0.005em;
  }

  &__sig {
    display: block;

    font-family: $mono;
    font-size: 0.5625rem;
    letter-spacing: 0.16em;
    text-transform: uppercase;
    color: $accent-deep;
  }
}

/* ==========================================================================
   СНОСКИ — кружок → полоса → текст
   ========================================================================== */

.anno {
  position: absolute;

  display: flex;
  align-items: flex-start;
  gap: 10px;

  max-width: 240px;

  z-index: 25;
  pointer-events: none;

  opacity: 0;

  .collage.is-visible & {
    animation: anno-in 0.7s $ease-soft both;
  }

  &__dot {
    flex: none;

    width: 7px;
    height: 7px;
    margin-top: 4px;

    border-radius: 50%;

    background-color: $text;
    box-shadow:
      0 0 0 3px rgba(242, 233, 220, 0.18),
      0 0 12px rgba(200, 135, 74, 0.45);
  }

  &__line {
    flex: none;

    width: 36px;
    height: 1px;
    margin-top: 7px;

    background-color: $text;
    opacity: 0.7;
  }

  &__text {
    display: flex;
    flex-direction: column;
    gap: 3px;

    min-width: 0;

    b {
      font-family: $mono;
      font-size: 0.5625rem;
      font-weight: 700;
      letter-spacing: 0.24em;
      text-transform: uppercase;

      color: $text;
      text-shadow: 0 1px 6px rgba(0, 0, 0, 0.55);
    }

    em {
      font-family: Georgia, "Times New Roman", serif;
      font-style: normal;
      font-size: 0.75rem;
      font-weight: 400;
      letter-spacing: 0.005em;
      line-height: 1.4;

      color: rgba(242, 233, 220, 0.88);
      text-shadow: 0 1px 6px rgba(0, 0, 0, 0.5);
    }
  }
}

/* --- позиции сносок внутри stage --- */

.anno--grid {
  left: 0;
  top: -1.5rem;

  .collage.is-visible & { animation-delay: 0.35s; }
}

.anno--portrait {
  left: 31%;
  top: 9%;

  .collage.is-visible & { animation-delay: 0.95s; }
}

.anno--landscape {
  left: 26%;
  bottom: 30%;

  .collage.is-visible & { animation-delay: 1.1s; }
}

.anno--square {
  right: 1%;
  top: 44%;

  .collage.is-visible & { animation-delay: 1.25s; }
}

.anno--tall {
  right: 22%;
  top: -1.5rem;

  .collage.is-visible & { animation-delay: 1.4s; }
}

.anno--tilt {
  left: 0;
  bottom: -0.5rem;

  .collage.is-visible & { animation-delay: 1.55s; }
}

.anno--note {
  right: 1%;
  bottom: 14%;

  .collage.is-visible & { animation-delay: 1.7s; }
}

/* ==========================================================================
   АДАПТИВ — уменьшаем ТОЛЬКО сцену (плитки + анкер)
   Сноски на мобилке скрываются полностью
   ========================================================================== */

@media (max-width: 1100px) {
  .collage__stage { zoom: 0.88; }
}

@media (max-width: 900px) {
  .collage__stage { zoom: 0.78; }
}

@media (max-width: 820px) {
  /* Сноски на мобилке не нужны — полностью убираем */
  .anno { display: none !important; }
}

@media (max-width: 720px) {
  .collage__stage { zoom: 0.66; }
}

@media (max-width: 560px) {
  .collage__stage { zoom: 0.55; }
}

@media (max-width: 440px) {
  .collage__stage { zoom: 0.46; }
}

@media (max-width: 360px) {
  .collage__stage { zoom: 0.40; }
}
</style>