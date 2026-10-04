<template>
  <section class="hero">
    <div class="hero__overlay" aria-hidden="true"></div>

    <div class="hero__left">
      <h1 class="hero__title">{{ name }}</h1>
      <p class="hero__subtitle">Фотоателье</p>
    </div>

    <aside class="hero__right">
      <span class="hero__line" aria-hidden="true"></span>

      <p class="hero__meta">
        <span class="hero__meta-row">Est. 2026</span>
        <span class="hero__meta-row">Портрет · Мода · Свет</span>
        <span class="hero__meta-row">Москва</span>
      </p>
    </aside>
  </section>
</template>

<script setup>
/**
 * 1.vue — hero.
 * Никаких «пилюль» и полос: снизу мягкий градиент-затемнение,
 * который растворяется в картинке. Текст читается сам собой.
 */

defineProps({
  name: {
    type: String,
    default: "Étude",
  },
});
</script>

<style scoped lang="scss">
@use "../styles/variables" as *;

/* ==========================================================================
   ЛОКАЛЬНЫЕ ПЕРЕМЕННЫЕ HERO
   ========================================================================== */

// --- Цвета ---
$text:   #493636;
$muted:  #ffff;

// --- Мягкая тень под текстом ---
$text-shadow: 0 1px 12px rgba(0, 0, 0, 0.35);

// --- Градиент снизу (главный герой) ---
// Начинается с прозрачного сверху, к низу — мягкое затемнение.
// Плавность задаётся процентами в linear-gradient.
$overlay-gradient: linear-gradient(
  to bottom,
  rgba(0, 0, 0, 0) 0%,
  rgba(0, 0, 0, 0) 40%,
  rgba(0, 0, 0, 0.25) 70%,
  rgba(0, 0, 0, 0.55) 100%
);

// --- Отступы ---
$padding-x:      8vw;
$padding-top:    8vh;
$padding-bottom: 8vh;
$gap-columns:    4vw;

// --- Заголовок ---
$title-size:      14vw;
$title-size-min:  3.5rem;
$title-size-max:  12rem;
$title-weight:    600;
$title-spacing:   -0.04em;
$title-leading:   0.9;

// --- Подпись «Фотоателье» ---
$subtitle-size:      0.875rem;
$subtitle-weight:    600;
$subtitle-spacing:   0.28em;
$subtitle-transform: uppercase;

// --- Мета-блок справа ---
$meta-size:      0.75rem;
$meta-weight:    600;
$meta-spacing:   0.2em;
$meta-transform: uppercase;
$meta-leading:   1.8;

// --- Декоративная линия ---
$line-width:   $size-1px;
$line-height:  6rem;
$line-opacity: 0.5;

/* ==========================================================================
   СТИЛИ
   ========================================================================== */

.hero {
  position: relative;

  display: flex;
  justify-content: space-between;
  align-items: stretch;

  width: $size-full;
  height: $size-full;

  padding: $padding-top $padding-x $padding-bottom;

  color: $text;

  // --- Градиент-подложка: лежит под всем, никого не сдвигает ---
  &__overlay {
    position: absolute;
    inset: $size-zero;

    background-image: $overlay-gradient;

    pointer-events: none;   // не мешает кликам
    z-index: $size-zero;    // под контентом
  }

  &__left,
  &__right {
    position: relative;     // приподнимаем над overlay
    z-index: 1;
  }

  &__left {
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    flex: $flex-grow;
    min-width: $size-zero;

    text-shadow: $text-shadow;
  }

  &__title {
    font-size: clamp($title-size-min, $title-size, $title-size-max);
    font-weight: $title-weight;
    letter-spacing: $title-spacing;
    line-height: $title-leading;
    margin-bottom: $space-sm;
    color: $text;
  }

  &__subtitle {
    font-size: $subtitle-size;
    font-weight: $subtitle-weight;
    letter-spacing: $subtitle-spacing;
    text-transform: $subtitle-transform;
    color: $muted;
  }

  &__right {
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    align-items: flex-end;
    gap: $space-md;

    flex: $flex-none;
    padding-left: $gap-columns;

    text-shadow: $text-shadow;
  }

  &__line {
    width: $line-width;
    height: $line-height;
    background-color: $text;
    opacity: $line-opacity;
  }

  &__meta {
    display: flex;
    flex-direction: column;
    gap: $space-sm;

    text-align: right;
    font-size: $meta-size;
    font-weight: $meta-weight;
    letter-spacing: $meta-spacing;
    text-transform: $meta-transform;
    line-height: $meta-leading;
    color: $muted;
  }

  &__meta-row {
    display: block;
    white-space: nowrap;
  }
}
</style>