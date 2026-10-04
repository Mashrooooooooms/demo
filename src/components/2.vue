<template>
  <section ref="root" class="phones" :class="{ 'is-visible': visible }">
    <!-- Градиент на фоне: слева тёмно → справа прозрачно -->
    <div class="phones__backdrop" aria-hidden="true"></div>

    <header class="phones__head">
      <span class="phones__label">03 — Фотостудия</span>
      <h2 class="phones__title">Сессии</h2>
    </header>

    <div class="phones__stage">
      <!-- ЛЕВЫЙ ТЕЛЕФОН — светлая тема -->
      <article class="phone phone--left">
        <div class="phone__frame">
          <div class="phone__screen">
            <div class="hero">
              <img class="hero__img" src="/portret.jpg" alt="Портрет">
              <div class="hero__notch"></div>

              <span class="hero__avatar" aria-hidden="true">
                <svg viewBox="0 0 40 40" width="100%" height="100%">
                  <rect width="40" height="40" fill="#b08968"/>
                  <circle cx="20" cy="15" r="7" fill="#f2e2cf"/>
                  <path d="M6 40c2-9 8-13 14-13s12 4 14 13z" fill="#f2e2cf"/>
                </svg>
              </span>

              <button class="hero__action" aria-label="Меню">◐</button>

              <div class="hero__title">
                <span class="hero__eyebrow">Фото</span>
                <span class="hero__display">Студия</span>
                <span class="hero__eyebrow hero__eyebrow--sub">Бронирование</span>
              </div>
            </div>

            <div class="body body--light">
              <div class="chips">
                <button
                  v-for="chip in leftChips"
                  :key="chip.id"
                  class="chip"
                  :class="{ 'chip--active': chip.id === leftActive.chip }"
                  @click="leftActive.chip = chip.id"
                >
                  {{ chip.label }}
                </button>
              </div>

              <div class="card card--light">
                <div class="card__label">
                  <span class="card__dot"></span>
                  Выберите дату съёмки
                </div>

                <div class="dates">
                  <button
                    v-for="d in leftDates"
                    :key="d.id"
                    class="date"
                    :class="{ 'date--active': d.id === leftActive.date }"
                    @click="leftActive.date = d.id"
                  >
                    <span class="date__num">{{ d.num }}</span>
                    <span class="date__day">{{ d.day }}</span>
                  </button>
                </div>

                <div class="card__label">
                  <span class="card__dot"></span>
                  Выберите время
                </div>

                <div class="slots">
                  <button
                    v-for="s in leftSlots"
                    :key="s.id"
                    class="slot"
                    :class="{ 'slot--active': s.id === leftActive.slot }"
                    @click="leftActive.slot = s.id"
                  >
                    {{ s.label }}
                  </button>
                </div>

                <div class="price">
                  <div class="price__col">
                    <span class="price__label">Стоимость</span>
                    <span class="price__value">4 450 ₽</span>
                  </div>
                  <button
                    class="btn btn--dark"
                    :class="{ 'is-pressed': leftActive.booked }"
                    @click="leftActive.booked = !leftActive.booked"
                  >
                    {{ leftActive.booked ? 'Забронировано' : 'Забронировать' }}
                  </button>
                </div>

                <p class="fineprint">
                  При подтверждении брони вносится депозит 50 % от суммы.
                  Остаток оплачивается после съёмки.
                </p>
              </div>
            </div>
          </div>
        </div>
      </article>

      <!-- ПРАВЫЙ ТЕЛЕФОН — тёмная тема -->
      <article class="phone phone--right">
        <div class="phone__frame">
          <div class="phone__screen">
            <div class="hero">
              <img class="hero__img" src="/transport.png" alt="Транспорт">
              <div class="hero__notch"></div>

              <span class="hero__avatar" aria-hidden="true">
                <svg viewBox="0 0 40 40" width="100%" height="100%">
                  <rect width="40" height="40" fill="#8a6f55"/>
                  <circle cx="20" cy="15" r="7" fill="#ead9c4"/>
                  <path d="M6 40c2-9 8-13 14-13s12 4 14 13z" fill="#ead9c4"/>
                </svg>
              </span>

              <div class="hero__title hero__title--left">
                <span class="hero__h1">Фотостудия</span>
                <span class="hero__h2">Лофт «Кадр»</span>
                <span class="hero__badge">Топ выбор</span>
              </div>
            </div>

            <div class="body body--dark">
              <div class="card card--dark">
                <div class="card__row">
                  <span class="card__title">Выберите зал</span>
                  <div class="tabs">
                    <button
                      class="tab"
                      :class="{ 'tab--active': rightActive.tab === 'studio' }"
                      @click="rightActive.tab = 'studio'"
                    >
                      A, C — студия
                    </button>
                    <button
                      class="tab"
                      :class="{ 'tab--active': rightActive.tab === 'hall' }"
                      @click="rightActive.tab = 'hall'"
                    >
                      B — зал
                    </button>
                  </div>
                </div>

                <div class="courts">
                  <button
                    v-for="room in rightRooms"
                    :key="room.id"
                    class="court"
                    :class="{ 'court--active': room.id === rightActive.room }"
                    @click="rightActive.room = room.id"
                  >
                    {{ room.id }}
                    <em v-if="room.premium">Премиум</em>
                  </button>
                </div>
              </div>

              <div class="card card--dark card--coach">
                <div class="coach__img">
                  <svg viewBox="0 0 80 80" width="100%" height="100%">
                    <rect width="80" height="80" fill="#2a3a20"/>
                    <circle cx="40" cy="30" r="14" fill="#cfe0a5"/>
                    <path d="M10 80c4-18 16-26 30-26s26 8 30 26z" fill="#cfe0a5"/>
                  </svg>
                </div>
                <div class="coach__body">
                  <div class="coach__title">Съёмка с фотографом.</div>
                  <p class="coach__text">Работаем с лучшими фотографами!</p>
                  <button
                    class="btn btn--accent"
                    :class="{ 'is-pressed': rightActive.coach }"
                    @click="rightActive.coach = !rightActive.coach"
                  >
                    {{ rightActive.coach ? 'Заказано' : 'Заказать съёмку' }}
                  </button>
                </div>
              </div>

              <button
                class="btn btn--wide btn--accent-soft"
                :class="{ 'is-pressed': rightActive.reserved }"
                @click="rightActive.reserved = !rightActive.reserved"
              >
                {{ rightActive.reserved ? 'Забронировано' : 'Забронировать' }}
              </button>

              <p class="fineprint fineprint--dark">
                Если вы хотите заказать фотографа в выбранный зал, сделайте это
                на этом шаге. Доступность залов указана на баннере выше.
              </p>

              <a class="subscribe" href="#">
                <span class="subscribe__heart">♥</span>
                Оформить подписку
              </a>
            </div>
          </div>
        </div>
      </article>
    </div>

    <!-- Подпись в правом нижнем углу — колонкой -->
    <div class="phones__sign">
      <span class="phones__sign-name">Лофт «Кадр»</span>
      <span class="phones__sign-line">Москва · ул. Большая Садовая, 3</span>
      <span class="phones__sign-line">Ежедневно, 10:00 — 22:00</span>
      <span class="phones__sign-line">+7 (495) 214‑78‑03</span>
    </div>
  </section>
</template>

<script setup>
import { reactive, ref, onMounted, onBeforeUnmount, nextTick } from 'vue'

/**
 * 2.vue — второй блок.
 * Два телефона со сдвигом по вертикали, подняты выше центра.
 * Левый: /portret.jpg  → светлая тема — бронь фотосессии.
 * Правый: /transport.png → тёмная тема — выбор зала / фотограф / бронь.
 * Фон — градиент: слева тёмно, справа прозрачно.
 *
 * Анимации — на CSS-@keyframes с fill-mode: both.
 * Класс .is-visible ставится/снимается через IntersectionObserver,
 * поэтому при каждом новом заходе секции во вьюпорт анимация
 * проигрывается с нуля.
 */

/* --- Lazy-animation trigger --- */

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

/* --- Левый телефон --- */

const leftChips = [
  { id: 'loft-b2',   label: 'Лофт B2'    },
  { id: 'studio-b1', label: 'Студия B1'  },
  { id: 'hall-a2',   label: 'Зал A2'     },
]

const leftDates = [
  { id: 'd13', num: '13', day: 'Пн' },
  { id: 'd14', num: '14', day: 'Вт' },
  { id: 'd17', num: '17', day: 'Пт' },
  { id: 'd19', num: '19', day: 'Вс' },
]

const leftSlots = [
  { id: 's1', label: '12:30 – 13:30' },
  { id: 's2', label: '13:45 – 14:45' },
]

const leftActive = reactive({
  chip:   'loft-b2',
  date:   'd13',
  slot:   's1',
  booked: false,
})

/* --- Правый телефон --- */

const rightRooms = [
  { id: 'A1', premium: false },
  { id: 'B1', premium: false },
  { id: 'B2', premium: false },
  { id: 'C1', premium: true  },
  { id: 'B3', premium: false },
]

const rightActive = reactive({
  tab:      'studio',
  room:     'B2',
  coach:    false,
  reserved: false,
})
</script>

<style scoped lang="scss">
@use "../styles/variables" as *;

/* ==========================================================================
   ПЕРЕМЕННЫЕ
   ========================================================================== */

// --- Цвета ---
$text:        #ffffff;
$text-dark:   #171717;
$muted:       rgba(255, 255, 255, 0.6);

$line:        rgba(255, 255, 255, 0.16);
$screen-bg:   #0e0e0e;
$card-light:  #f4efe6;
$card-dark:   #1c1c1e;

$accent:      #c8d96f;
$accent-soft: #d6e39a;
$ink:         #161616;

// --- Отступы блока ---
$padding-x:      6vw;
$padding-top:    5vh;
$padding-bottom: 5vh;

// --- Шапка блока / подпись ---
$label-size:      0.6875rem;
$label-spacing:   0.28em;
$label-weight:    600;

$title-size:    2.5rem;
$title-weight:  300;
$title-spacing: -0.02em;

// --- Фоновый градиент ---
$grad-from:  rgba(10, 10, 14, 0.92);
$grad-mid:   rgba(10, 10, 14, 0.55);
$grad-to:    rgba(10, 10, 14, 0.0);

// --- Сцена ---
$stage-gap:   3vw;

// --- Телефон ---
$phone-width:   300px;
$phone-ratio:   9 / 19.5;
$phone-radius:  44px;
$frame-pad:     8px;
$screen-radius: 38px;

// --- Смещения телефонов ---
$offset-left:   -10vh;
$offset-right:    2vh;

// --- Внутри экрана ---
$radius-card:   22px;
$radius-inner:  14px;
$radius-chip:   999px;

// --- Анимация: мягкая, нежная ---
$ease-soft: cubic-bezier(0.25, 0.46, 0.45, 0.94);

/* ==========================================================================
   KEYFRAMES — плавные, с минимальной амплитудой
   ========================================================================== */

@keyframes fade-up {
  from { opacity: 0; transform: translateY(14px); }
  to   { opacity: 1; transform: translateY(0);    }
}

@keyframes fade-down {
  from { opacity: 0; transform: translateY(-10px); }
  to   { opacity: 1; transform: translateY(0);     }
}

@keyframes fade-in {
  from { opacity: 0; }
  to   { opacity: 1; }
}

@keyframes zoom-in {
  from { opacity: 0; transform: scale(1.05); }
  to   { opacity: 1; transform: scale(1);    }
}

@keyframes phone-in {
  from { opacity: 0; transform: translateY(20px) scale(1.04); }
  to   { opacity: 1; transform: translateY(0)    scale(1);    }
}

@keyframes img-in {
  from { transform: scale(1.06); }
  to   { transform: scale(1);    }
}

/* ==========================================================================
   БЛОК
   ========================================================================== */

.phones {
  position: relative;

  display: flex;
  flex-direction: column;

  width: $size-full;
  height: $size-full;

  padding: $padding-top $padding-x $padding-bottom;

  color: $text;

  overflow: hidden;

  // --- Мобильное масштабирование ---
  @media (max-width: 1100px) { zoom: 0.88; }
  @media (max-width:  900px) { zoom: 0.78; }
  @media (max-width:  720px) { zoom: 0.66; }
  @media (max-width:  560px) { zoom: 0.55; }
  @media (max-width:  440px) { zoom: 0.46; }
  @media (max-width:  360px) { zoom: 0.40; }

  // --- Градиент слева-направо ---
  &__backdrop {
    position: absolute;
    inset: $size-zero;

    background: linear-gradient(
      to right,
      $grad-from 0%,
      $grad-mid 45%,
      $grad-to 100%
    );

    pointer-events: none;
    z-index: $size-zero;

    opacity: 0;
    .phones.is-visible & {
      animation: fade-in 1.4s $ease-soft 0.05s both;
    }
  }

  &__head {
    position: relative;
    z-index: 1;

    display: flex;
    flex-direction: column;
    gap: $space-sm;

    flex: $flex-none;
    margin-bottom: 3vh;

    > * {
      opacity: 0;
    }

    .phones.is-visible & > * {
      animation: fade-down 0.9s $ease-soft both;
    }

    .phones.is-visible & > *:nth-child(1) { animation-delay: 0.15s; }
    .phones.is-visible & > *:nth-child(2) { animation-delay: 0.28s; }
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
  }

  &__stage {
    position: relative;
    z-index: 1;

    flex: $flex-grow;
    min-height: $size-zero;

    display: flex;
    justify-content: center;
    align-items: center;
    gap: $stage-gap;
  }

  // --- Подпись в правом нижнем углу: колонка ---
  &__sign {
    position: absolute;
    right:  $padding-x;
    bottom: $padding-bottom;

    display: flex;
    flex-direction: column;
    align-items: flex-end;
    gap: 2px;

    text-align: right;

    z-index: 2;
    pointer-events: none;

    opacity: 0;
    .phones.is-visible & {
      animation: fade-in 1s $ease-soft 1.3s both;
    }

    &-name {
      color: $text;
    }

    &-line {
      color: $muted;
    }
  }
}

/* ==========================================================================
   ТЕЛЕФОН
   ========================================================================== */

.phone {
  flex: $flex-none;
  width: $phone-width;

  &--left  { transform: translateY($offset-left); }
  &--right { transform: translateY($offset-right); }

  &__frame {
    padding: $frame-pad;

    background-color: #050505;
    border-radius: $phone-radius;

    box-shadow:
      0 30px 60px rgba(0, 0, 0, 0.45),
      0 0 0 1px rgba(255, 255, 255, 0.06) inset;

    opacity: 0;
  }

  // ВАЖНО: .phones.is-visible — предок, поэтому он идёт первым в селекторе.
  // Раньше было наоборот (`&--left .phones.is-visible &__frame`), из-за чего
  // ни один селектор не матчился и контент оставался с opacity: 0.
  .phones.is-visible &--left &__frame {
    animation: phone-in 1.2s $ease-soft 0.4s both;
  }

  .phones.is-visible &--right &__frame {
    animation: phone-in 1.2s $ease-soft 0.6s both;
  }

  &__screen {
    position: relative;

    width: $size-full;
    aspect-ratio: $phone-ratio;

    background-color: $screen-bg;
    border-radius: $screen-radius;

    overflow: hidden;
  }
}

/* ==========================================================================
   HERO
   ========================================================================== */

.hero {
  position: relative;

  width: $size-full;
  height: 48%;

  overflow: hidden;

  &__img {
    position: absolute;
    inset: $size-zero;

    width: $size-full;
    height: $size-full;

    object-fit: cover;

    filter: brightness(0.85);

    transform: scale(1.06);
    .phones.is-visible & {
      animation: img-in 2.2s $ease-soft 0.5s both;
    }
  }

  &::after {
    content: "";
    position: absolute;
    inset: $size-zero;

    background: linear-gradient(
      to bottom,
      rgba(0, 0, 0, 0.35) 0%,
      rgba(0, 0, 0, 0.0)  35%,
      rgba(0, 0, 0, 0.55) 100%
    );

    pointer-events: none;
  }

  &__notch {
    position: absolute;
    top: 12px;
    left: 50%;
    transform: translateX(-50%);

    width: 84px;
    height: 22px;

    background-color: #050505;
    border-radius: $radius-chip;

    z-index: 3;

    opacity: 0;
    .phones.is-visible & {
      animation: fade-in 0.9s $ease-soft 0.9s both;
    }
  }

  &__avatar {
    position: absolute;
    top: 12px;
    left: 14px;

    display: block;

    width: 34px;
    height: 34px;

    border: 2px solid rgba(255, 255, 255, 0.7);
    border-radius: 50%;

    overflow: hidden;
    z-index: 3;

    opacity: 0;
    .phones.is-visible & {
      animation: fade-in 0.9s $ease-soft 1s both;
    }
  }

  &__action {
    position: absolute;
    top: 12px;
    right: 14px;

    display: grid;
    place-items: center;

    width: 34px;
    height: 34px;

    padding: $size-zero;

    background-color: rgba(255, 255, 255, 0.15);
    border: 1px solid rgba(255, 255, 255, 0.3);
    border-radius: 50%;

    color: $text;
    font-size: 14px;

    backdrop-filter: blur(6px);
    -webkit-backdrop-filter: blur(6px);

    cursor: pointer;
    z-index: 3;

    opacity: 0;
    .phones.is-visible & {
      animation: fade-in 0.9s $ease-soft 1s both;
    }
  }

  &__title {
    position: absolute;
    left: 0;
    right: 0;
    bottom: 22px;

    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 2px;

    padding: 0 18px;

    text-align: center;
    z-index: 2;

    opacity: 0;
    .phones.is-visible & {
      animation: fade-up 1s $ease-soft 1.05s both;
    }

    &--left {
      align-items: flex-start;
      text-align: left;
    }
  }

  &__eyebrow {
    font-size: 0.625rem;
    font-weight: 600;
    letter-spacing: 0.32em;
    text-transform: uppercase;
    color: rgba(255, 255, 255, 0.85);

    &--sub {
      margin-top: 2px;
    }
  }

  &__display {
    font-family: Georgia, "Times New Roman", serif;
    font-size: 2.25rem;
    font-weight: 700;
    letter-spacing: 0.02em;
    line-height: 1;

    color: #f0d9b5;
    text-shadow: 0 2px 12px rgba(0, 0, 0, 0.45);
  }

  &__h1 {
    font-size: 1.25rem;
    font-weight: 500;
    letter-spacing: -0.01em;
    color: $text;
  }

  &__h2 {
    font-size: 1.125rem;
    font-weight: 400;
    color: rgba(255, 255, 255, 0.85);
  }

  &__badge {
    margin-top: 8px;

    padding: 4px 12px;

    font-size: 0.625rem;
    font-weight: 600;
    letter-spacing: 0.08em;
    color: $ink;

    background-color: $accent;
    border-radius: $radius-chip;

    opacity: 0;
    .phones.is-visible & {
      animation: fade-in 0.9s $ease-soft 1.35s both;
    }
  }
}

/* ==========================================================================
   НИЗ ЭКРАНА
   ========================================================================== */

.body {
  position: relative;

  height: 52%;

  display: flex;
  flex-direction: column;
  gap: 10px;

  padding: 12px;

  overflow: hidden;

  &--light { background-color: $card-light; color: $text-dark; }
  &--dark  { background-color: #101012;     color: $text; }

  > * {
    opacity: 0;
  }

  // ВАЖНО: .phones.is-visible — предок, поэтому он идёт первым.
  // Раньше было `.phone--left .phones.is-visible & > *:nth-child(1)`,
  // что компилировалось в несуществующую цепочку DOM.

  .phones.is-visible .phone--left & > *:nth-child(1) {
    animation: fade-up 0.85s $ease-soft 0.85s both;
  }
  .phones.is-visible .phone--left & > *:nth-child(2) {
    animation: fade-up 0.85s $ease-soft 0.98s both;
  }
  .phones.is-visible .phone--left & > *:nth-child(3) {
    animation: fade-up 0.85s $ease-soft 1.11s both;
  }
  .phones.is-visible .phone--left & > *:nth-child(4) {
    animation: fade-up 0.85s $ease-soft 1.24s both;
  }
  .phones.is-visible .phone--left & > *:nth-child(5) {
    animation: fade-up 0.85s $ease-soft 1.37s both;
  }

  .phones.is-visible .phone--right & > *:nth-child(1) {
    animation: fade-up 0.85s $ease-soft 1.05s both;
  }
  .phones.is-visible .phone--right & > *:nth-child(2) {
    animation: fade-up 0.85s $ease-soft 1.18s both;
  }
  .phones.is-visible .phone--right & > *:nth-child(3) {
    animation: fade-up 0.85s $ease-soft 1.31s both;
  }
  .phones.is-visible .phone--right & > *:nth-child(4) {
    animation: fade-up 0.85s $ease-soft 1.44s both;
  }
  .phones.is-visible .phone--right & > *:nth-child(5) {
    animation: fade-up 0.85s $ease-soft 1.57s both;
  }
}

/* ==========================================================================
   ЧИПСЫ
   ========================================================================== */

.chips {
  display: flex;
  gap: 6px;

  overflow-x: auto;
  scrollbar-width: none;

  &::-webkit-scrollbar { display: none; }
}

.chip {
  flex: $flex-none;

  padding: 7px 12px;

  font-size: 0.6875rem;
  font-weight: 500;
  white-space: nowrap;

  background-color: rgba(0, 0, 0, 0.06);
  color: rgba(23, 23, 23, 0.7);
  border: $size-1px solid rgba(0, 0, 0, 0.08);
  border-radius: $radius-chip;

  cursor: pointer;
  transition: background-color 0.2s ease, color 0.2s ease;

  &--active {
    background-color: $accent;
    color: $ink;
    border-color: $accent;
  }
}

/* ==========================================================================
   КАРТОЧКА
   ========================================================================== */

.card {
  padding: 14px;

  border-radius: $radius-card;

  &--light {
    background-color: #ffffff;
    color: $text-dark;
    box-shadow: 0 6px 20px rgba(0, 0, 0, 0.08);
  }

  &--dark {
    background-color: $card-dark;
    color: $text;
    border: $size-1px solid rgba(255, 255, 255, 0.06);
  }

  &__label {
    display: flex;
    align-items: center;
    gap: 6px;

    margin-bottom: 10px;

    font-size: 0.6875rem;
    font-weight: 500;
    color: rgba(23, 23, 23, 0.55);
  }

  &__dot {
    width: 8px;
    height: 8px;

    border: 1.5px solid rgba(23, 23, 23, 0.35);
    border-radius: 50%;
  }

  &__row {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 8px;

    margin-bottom: 10px;
  }

  &__title {
    font-size: 0.8125rem;
    font-weight: 600;
  }
}

/* ==========================================================================
   ДАТЫ
   ========================================================================== */

.dates {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 6px;

  margin-bottom: 14px;
}

.date {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2px;

  padding: 12px 0;

  background-color: #f0ebe1;
  border: $size-1px solid transparent;
  border-radius: $radius-inner;

  cursor: pointer;
  transition:
    background-color 0.25s ease,
    border-color     0.25s ease;

  &--active {
    background-color: #ffffff;
    border-color: $ink;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
  }

  &__num {
    font-size: 1rem;
    font-weight: 600;
    color: $text-dark;
  }

  &__day {
    font-size: 0.625rem;
    color: rgba(23, 23, 23, 0.5);
  }
}

/* ==========================================================================
   СЛОТЫ
   ========================================================================== */

.slots {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 6px;

  margin-bottom: 14px;
}

.slot {
  padding: 12px 8px;

  font-size: 0.75rem;
  font-weight: 500;
  color: rgba(23, 23, 23, 0.65);

  background-color: #f0ebe1;
  border: $size-1px solid transparent;
  border-radius: $radius-inner;

  cursor: pointer;
  transition:
    background-color 0.25s ease,
    border-color     0.25s ease,
    color            0.25s ease;

  &--active {
    background-color: #ffffff;
    border-color: $ink;
    color: $text-dark;
  }
}

/* ==========================================================================
   ЦЕНА
   ========================================================================== */

.price {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;

  margin-bottom: 12px;

  &__col {
    display: flex;
    flex-direction: column;
    gap: 2px;
  }

  &__label {
    font-size: 0.6875rem;
    color: rgba(23, 23, 23, 0.5);
  }

  &__value {
    font-size: 1.125rem;
    font-weight: 600;
    color: $text-dark;
  }
}

/* ==========================================================================
   ТАБЫ
   ========================================================================== */

.tabs {
  display: flex;
  gap: 8px;

  font-size: 0.625rem;
  letter-spacing: 0.02em;
}

.tab {
  padding: $size-zero;

  font-size: inherit;
  color: rgba(255, 255, 255, 0.5);

  background: transparent;
  border: $size-zero;

  cursor: pointer;
  transition: color 0.25s ease;

  &--active {
    color: $text;
    font-weight: 600;
  }
}

/* ==========================================================================
   СЕТКА ЗАЛОВ
   ========================================================================== */

.courts {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 6px;
}

.court {
  position: relative;

  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: center;
  gap: 4px;

  padding: 14px 10px;
  min-height: 62px;

  font-size: 0.875rem;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.85);

  background-color: #26262a;
  border: $size-1px solid transparent;
  border-radius: $radius-inner;

  cursor: pointer;
  text-align: left;
  transition:
    border-color     0.25s ease,
    background-color 0.25s ease;

  em {
    font-size: 0.5625rem;
    font-style: normal;
    font-weight: 500;
    letter-spacing: 0.06em;
    text-transform: uppercase;

    padding: 2px 6px;

    background-color: rgba(200, 217, 111, 0.75);
    color: $ink;
    border-radius: $radius-chip;
  }

  &--active {
    border-color: $accent;
    box-shadow: 0 0 0 1px $accent inset;

    &::after {
      content: "";
      position: absolute;
      top: 8px;
      right: 8px;

      width: 8px;
      height: 8px;

      background-color: $accent;
      border-radius: 50%;

      animation: zoom-in 0.4s $ease-soft;
    }
  }
}

/* ==========================================================================
   ФОТОГРАФ
   ========================================================================== */

.card--coach {
  display: flex;
  gap: 10px;

  padding: 10px;
}

.coach {
  &__img {
    flex: $flex-none;

    width: 66px;
    height: 66px;

    border-radius: $radius-inner;
    overflow: hidden;
  }

  &__body {
    display: flex;
    flex-direction: column;
    gap: 4px;

    min-width: $size-zero;
  }

  &__title {
    font-size: 0.75rem;
    font-weight: 600;
    line-height: 1.25;
  }

  &__text {
    font-size: 0.625rem;
    color: rgba(255, 255, 255, 0.55);
  }
}

/* ==========================================================================
   КНОПКИ
   ========================================================================== */

.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;

  padding: 10px 18px;

  font-size: 0.75rem;
  font-weight: 600;
  letter-spacing: 0.01em;

  border: $size-1px solid transparent;
  border-radius: $radius-chip;

  cursor: pointer;
  transition:
    filter           0.25s ease,
    background-color 0.35s $ease-soft,
    color            0.35s $ease-soft,
    transform        0.25s ease;

  &:hover { filter: brightness(1.06); }
  &:active { transform: translateY(1px); }

  &--dark {
    background-color: $ink;
    color: $text;
  }

  &--accent {
    align-self: flex-start;

    padding: 6px 12px;

    font-size: 0.625rem;

    background-color: $accent;
    color: $ink;
  }

  &--accent-soft {
    background-color: $accent-soft;
    color: $ink;
  }

  &--wide {
    width: $size-full;

    padding: 14px 18px;

    font-size: 0.8125rem;
  }

  &.is-pressed {
    background-color: $accent;
    color: $ink;
  }
}

/* ==========================================================================
   МЕЛКИЙ ТЕКСТ / ПОДПИСКА
   ========================================================================== */

.fineprint {
  margin: $size-zero;

  font-size: 0.5625rem;
  line-height: 1.5;
  text-align: center;
  color: rgba(23, 23, 23, 0.45);

  &--dark {
    color: rgba(255, 255, 255, 0.4);
    text-align: center;
  }
}

.subscribe {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 6px;

  margin-top: auto;
  padding: 8px 0 2px;

  font-size: 0.6875rem;
  font-weight: 600;
  letter-spacing: 0.06em;
  text-transform: uppercase;

  color: $accent;
  text-decoration: none;

  transition: opacity 0.3s ease;

  &:hover { opacity: 0.75; }

  &__heart {
    font-size: 0.875rem;
  }
}
</style>