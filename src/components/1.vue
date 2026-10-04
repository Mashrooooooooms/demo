<template>
  <section class="hero">
    <div class="hero__overlay" aria-hidden="true"></div>

    <!-- ================================================================
         СНОСКИ: кружок → полоса → текст
         ================================================================ -->

    <!-- НАД правым верхом — фон -->
    <div class="anno anno--bg anno--right">
      <span class="anno__dot"></span>
      <span class="anno__line"></span>
      <span class="anno__text">
        <b>Фон</b>
        <em>Градиент: тёмный низ, светлый верх — для читаемости заголовка и подзаголовка.</em>
      </span>
    </div>

    <!-- В центре пустого пространства — воздух -->
    <div class="anno anno--air">
      <span class="anno__dot"></span>
      <span class="anno__line"></span>
      <span class="anno__text">
        <b>Воздух</b>
        <em>Больше половины плоскости — свободно. Композиция дышит.</em>
      </span>
    </div>

    <!-- СЛЕВА от meta-блока, ниже -->
    <div class="anno anno--meta anno--right">
      <span class="anno__dot"></span>
      <span class="anno__line"></span>
      <span class="anno__text">
        <b>Информация</b>
        <em>Тот же контрастный цвет — для правильного восприятия.</em>
      </span>
    </div>

    <!-- ================================================================
         КОНТЕНТ
         ================================================================ -->

    <div class="hero__left">
      <!-- Блок заголовка + сноска справа -->
      <div class="hero__text-block">
        <h1 class="hero__title">{{ name }}</h1>
        <div class="anno anno--type anno--side">
          <span class="anno__dot"></span>
          <span class="anno__line"></span>
          <span class="anno__text">
            <b>Заголовок</b>
            <em>Стильный, броский, большой — привлекает внимание.</em>
          </span>
        </div>
      </div>

      <!-- Блок подзаголовка + сноска справа -->
      <div class="hero__text-block">
        <p class="hero__subtitle">Фотоателье</p>
        <div class="anno anno--sub anno--side">
          <span class="anno__dot"></span>
          <span class="anno__line"></span>
          <span class="anno__text">
            <b>Подзаголовок</b>
            <em>Контрастный светлый цвет — ведёт внимание в нужную сторону.</em>
          </span>
        </div>
      </div>
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
 * Сноски: заголовок и подзаголовок — справа от текста,
 * выровнены по одному левому краю (друг напротив друга по вертикали),
 * доп. информация — справа от кружка и полосы.
 * В центре — сноска про воздух.
 * Сноска "Информация" смещена влево от meta-блока и опущена ниже.
 * Сноска "Заголовок" смещена вниз на 3rem от центра,
 * сноска "Подзаголовок" — на 1.5rem от центра (чуть выше заголовка).
 * Градиент снизу чуть темнее.
 *
 * На мобилке:
 *  · тёмная часть занимает больше половины экрана;
 *  · сноски полностью скрываются;
 *  · у .hero нет собственного скролла — иначе он перехватывает
 *    touch-жест и блокирует scroll-snap у родителя (.main__content).
 *    Вместо этого блок ровно занимает свою ячейку grid (height: 100%).
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

$text:   #493636;
$muted:  #ffff;

$text-shadow: 0 1px 12px rgba(0, 0, 0, 0.35);

// --- Градиент: чуть темнее снизу ---
$overlay-gradient: linear-gradient(
  to bottom,
  rgba(0, 0, 0, 0) 0%,
  rgba(0, 0, 0, 0) 35%,
  rgba(0, 0, 0, 0.35) 65%,
  rgba(0, 0, 0, 0.75) 100%
);

// --- Мобильный градиент: тёмное занимает больше половины ---
$overlay-gradient-mobile: linear-gradient(
  to bottom,
  rgba(0, 0, 0, 0) 0%,
  rgba(0, 0, 0, 0.15) 25%,
  rgba(0, 0, 0, 0.5) 50%,
  rgba(0, 0, 0, 0.75) 75%,
  rgba(0, 0, 0, 0.9) 100%
);

$padding-x:      8vw;
$padding-top:    8vh;
$padding-bottom: 8vh;
$gap-columns:    4vw;

$title-size:      14vw;
$title-size-min:  3.5rem;
$title-size-max:  12rem;
$title-weight:    600;
$title-spacing:   -0.04em;
$title-leading:   0.9;

$subtitle-size:      0.875rem;
$subtitle-weight:    600;
$subtitle-spacing:   0.28em;
$subtitle-transform: uppercase;

$meta-size:      0.75rem;
$meta-weight:    600;
$meta-spacing:   0.2em;
$meta-transform: uppercase;
$meta-leading:   1.8;

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

  &__overlay {
    position: absolute;
    inset: $size-zero;

    background-image: $overlay-gradient;

    pointer-events: none;
    z-index: $size-zero;
  }

  &__left,
  &__right {
    position: relative;
    z-index: 1;
  }

  &__left {
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    gap: 0.25rem;

    flex: $flex-grow;
    min-width: $size-zero;

    text-shadow: $text-shadow;
  }

  /* Обёртка для текста + сноски */
  &__text-block {
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: flex-start;

    width: max-content; /* важно: ширина по контенту, чтобы сноска встала ровно за текстом */
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

/* ==========================================================================
   СНОСКИ — кружок → полоса → текст (белые)
   ========================================================================== */

.anno {
  position: absolute;

  display: flex;
  align-items: flex-start;
  gap: 10px;

  max-width: 260px;

  z-index: 5;
  pointer-events: none;

  &__dot {
    flex: none;

    width: 7px;
    height: 7px;
    margin-top: 4px;

    border-radius: 50%;

    background-color: #ffffff;
    box-shadow:
      0 0 0 3px rgba(255, 255, 255, 0.18),
      0 0 12px rgba(255, 255, 255, 0.4);
  }

  &__line {
    flex: none;

    width: 36px;
    height: 1px;
    margin-top: 7px;

    background-color: #ffffff;
    opacity: 0.75;
  }

  &__text {
    display: flex;
    flex-direction: column;
    gap: 3px;

    min-width: 0;

    b {
      font-family: "IBM Plex Mono", ui-monospace, monospace;
      font-size: 0.5625rem;
      font-weight: 700;
      letter-spacing: 0.24em;
      text-transform: uppercase;

      color: #ffffff;
      text-shadow: 0 1px 6px rgba(0, 0, 0, 0.6);
    }

    em {
      font-family: Georgia, "Times New Roman", serif;
      font-style: normal;
      font-size: 0.75rem;
      font-weight: 400;
      letter-spacing: 0.005em;
      line-height: 1.4;

      color: rgba(255, 255, 255, 0.88);
      text-shadow: 0 1px 6px rgba(0, 0, 0, 0.55);
    }
  }

  /* зеркальный — точка и полоса справа */
  &--right {
    flex-direction: row-reverse;

    .anno__text {
      align-items: flex-end;
      text-align: right;
    }
  }
}

/* ==========================================================================
   СНОСКИ СПРАВА ОТ ТЕКСТА (Заголовок и Подзаголовок)
   Привязаны к .hero__text-block через left: 100%
   ========================================================================== */

.anno--side {
  position: absolute;
  left: 100%;
  margin-left: 1.5rem; /* отступ от текста */
  /* Базовая точка привязки — центр текстового блока */
  top: 50%;
  transform: translateY(-50%);

  width: max-content;
  max-width: 260px;

  .anno__text {
    align-items: flex-start;
    text-align: left;
  }
}

/* Заголовок — опущен ниже центра на 3rem */
.anno--type {
  top: calc(50% + 3rem);
}

/* Подзаголовок — опущен ниже центра на 1.5rem (чуть ниже) */
.anno--sub {
  top: calc(50% + 1.5rem);
}

/* --- позиции --- */

/* Фон — правый верхний угол */
.anno--bg {
  top: 8vh;
  right: 8vw;
}

/* Воздух — по центру пустой зоны */
.anno--air {
  top: 30%;
  left: 50%;
  transform: translateX(-50%);
}

/* Информация — СЛЕВА от meta-блока, ниже */
.anno--meta {
  /* Сдвигаем влево от правого края, чтобы не перекрывать meta-блок.
     Значение 14rem подобрано с учётом ширины блока meta */
  right: calc(8vw + 14rem);
  /* Опускаем ниже, выравнивая по нижнему краю meta-блока */
  bottom: calc(8vh + 1rem);
}

/* ==========================================================================
   МОБИЛЬНАЯ ВЕРСИЯ
   ========================================================================== */

@media (max-width: 820px) {
  .hero {
    flex-direction: column;
    justify-content: flex-end;   /* контент прижат к низу */
    height: 100%;                /* ровно ячейка grid, без auto */
    min-height: 0;               /* не тянем блок выше */
    padding: 6vh 6vw;

    /* ВАЖНО: собственный скролл у hero НЕ заводим.
       overflow-y: auto + overscroll-behavior: contain перехватывают
       touch-жест и ломают scroll-snap у .main__content. */
  }

  /* --- Тёмный градиент выше: > половины экрана --- */
  .hero__overlay {
    background-image: $overlay-gradient-mobile;
  }

  /* --- Сноски на мобилке полностью скрываем --- */
  .anno {
    display: none !important;
  }

  .hero__left {
    justify-content: flex-end;
  }

  .hero__text-block {
    position: static;
    width: auto;
  }

  .hero__right {
    margin-top: 28px;
    padding-left: 0;
    align-items: flex-start;
    text-align: left;
  }

  .hero__meta {
    text-align: left;
  }
}
</style>