<template>
  <footer ref="root" class="foot" :class="{ 'is-visible': visible }">
    <div class="foot__backdrop" aria-hidden="true"></div>

    <!-- Верхний кикер -->
    <div class="foot__kicker">
      <span class="foot__kicker-num">07</span>
      <span class="foot__kicker-text">Колофон · Студия</span>
      <span class="foot__kicker-line"></span>
      <span class="foot__kicker-meta">Moscow · MMXXVI</span>
    </div>

    <!-- Основная сетка -->
    <div class="foot__grid">
      <!-- 01 — Бренд -->
      <div class="foot__col foot__col--brand">
        <span class="foot__mark">
          KADR<span class="foot__mark-dot">·</span>DEV
        </span>

        <p class="foot__tagline">
          Студия заказной разработки. Собираем сайты, CRM-системы
          и телеграм-ботов для бизнеса, который устал от шаблонов.
        </p>

        <ul class="badges">
          <li class="badges__item">
            <span class="badges__dot"></span>
            Открыты для проектов
          </li>
          <li class="badges__item">
            <span class="badges__dot"></span>
            Работаем с 2020
          </li>
          <li class="badges__item">
            <span class="badges__dot"></span>
            Удалённо · по всей РФ
          </li>
        </ul>
      </div>

      <!-- 02 — Услуги -->
      <nav class="foot__col foot__col--nav">
        <span class="foot__label">Услуги</span>
        <ul class="foot__list">
          <li><a href="#" class="foot__link">Лендинги<span>01</span></a></li>
          <li><a href="#" class="foot__link">Корпоративные сайты<span>02</span></a></li>
          <li><a href="#" class="foot__link">CRM и админ-панели<span>03</span></a></li>
          <li><a href="#" class="foot__link">Telegram и VK боты<span>04</span></a></li>
          <li><a href="#" class="foot__link">Интеграции и API<span>05</span></a></li>
          <li><a href="#" class="foot__link">Дизайн и прототипы<span>06</span></a></li>
        </ul>
      </nav>

      <!-- 03 — Разделы -->
      <nav class="foot__col foot__col--nav">
        <span class="foot__label">Разделы</span>
        <ul class="foot__list">
          <li><a href="#hero"    class="foot__link">Начало<span>01</span></a></li>
          <li><a href="#cases"   class="foot__link">Работы<span>02</span></a></li>
          <li><a href="#collage" class="foot__link">Коллаж<span>03</span></a></li>
          <li><a href="#crm"     class="foot__link">Аналитика<span>04</span></a></li>
          <li><a href="#contact" class="foot__link">Контакты<span>05</span></a></li>
        </ul>
      </nav>

      <!-- 04 — Контакты + CTA -->
      <div class="foot__col foot__col--contacts">
        <span class="foot__label">Связь</span>

        <ul class="foot__list foot__list--contacts">
          <li>
            <a href="https://t.me/kadr_dev" class="contact" target="_blank">
              <span class="contact__label">Telegram</span>
              <span class="contact__val">@kadr_dev</span>
              <span class="contact__arrow">↗</span>
            </a>
          </li>
          <li>
            <a href="mailto:hello@kadr-dev.ru" class="contact">
              <span class="contact__label">Почта</span>
              <span class="contact__val">hello@kadr-dev.ru</span>
              <span class="contact__arrow">↗</span>
            </a>
          </li>
          <li>
            <a href="tel:+79990000000" class="contact">
              <span class="contact__label">Телефон</span>
              <span class="contact__val">+7 (999) 000-00-00</span>
              <span class="contact__arrow">↗</span>
            </a>
          </li>
        </ul>

        <a href="#contact" class="cta">
          <span>Обсудить проект</span>
          <span class="cta__arrow">→</span>
        </a>
      </div>
    </div>

    <!-- Нижняя полоса -->
    <div class="foot__bottom">
      <span class="foot__copy">© 2026 Kadr Development</span>

      <span class="foot__legal">
        <a href="/privacy" class="foot__legal-link">Политика конфиденциальности</a>
        <span class="foot__legal-sep">·</span>
        <span class="foot__legal-text">ИНН 7700000000 · ОГРН 0000000000000</span>
      </span>

      <a href="#hero" class="foot__up" aria-label="Наверх">
        <span class="foot__up-label">Наверх</span>
        <span class="foot__up-arrow">↑</span>
      </a>
    </div>
  </footer>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

/**
 * Footer — колофон.
 * Четыре колонки: бренд + бейджи, услуги, разделы, контакты + CTA.
 * Нижняя полоса: копирайт, юр. информация, ссылка наверх.
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
    ([entry]) => {
      if (entry.isIntersecting) visible.value = true
    },
    { threshold: 0.15 }
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
$muted-2:     rgba(244, 236, 223, 0.32);

$hairline:    rgba(200, 170, 135, 0.16);
$hairline-2:  rgba(200, 170, 135, 0.08);
$faint:       rgba(200, 170, 135, 0.10);

$accent:      #c8874a;
$accent-deep: #8a5a2c;
$espresso:    #100a06;

$serif: Georgia, "Times New Roman", serif;
$mono: "IBM Plex Mono", "JetBrains Mono", ui-monospace,
       SFMono-Regular, Menlo, Consolas, monospace;

$padding-x:      5vw;
$padding-top:    40px;
$padding-bottom: 22px;

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

.foot {
  position: relative;

  padding: $padding-top $padding-x $padding-bottom;

  color: $text;

  background-color: $espresso;

  border-top: 1px solid $hairline;

  overflow: hidden;

  &__backdrop {
    position: absolute;
    inset: 0;

    background:
      radial-gradient(
        60% 80% at 100% 0%,
        rgba(200, 135, 74, 0.10) 0%,
        rgba(200, 135, 74, 0.0) 60%
      ),
      radial-gradient(
        60% 80% at 0% 100%,
        rgba(120, 80, 50, 0.14) 0%,
        rgba(120, 80, 50, 0.0) 60%
      );

    pointer-events: none;
    z-index: 0;
  }

  /* ---------------------------------------------------------------------
     Кикер
     --------------------------------------------------------------------- */

  &__kicker {
    position: relative;
    z-index: 1;

    display: flex;
    align-items: center;
    gap: 14px;

    padding-bottom: 16px;
    margin-bottom: 28px;

    border-bottom: 1px solid $hairline;

    font-family: $mono;
    font-size: 0.625rem;
    letter-spacing: 0.24em;
    text-transform: uppercase;

    opacity: 0;
    .foot.is-visible & {
      animation: fade-down 0.8s $ease-soft 0.1s both;
    }
  }

  &__kicker-num {
    font-weight: 700;
    color: $accent;
  }

  &__kicker-text {
    color: $muted;
  }

  &__kicker-line {
    flex: 1 1 auto;
    height: 1px;
    background: $hairline;
  }

  &__kicker-meta {
    color: $muted-2;
  }

  /* ---------------------------------------------------------------------
     Сетка колонок
     --------------------------------------------------------------------- */

  &__grid {
    position: relative;
    z-index: 1;

    display: grid;
    grid-template-columns: 1.5fr 1fr 1fr 1.3fr;
    gap: 40px;

    padding-bottom: 36px;
    margin-bottom: 22px;

    border-bottom: 1px solid $hairline;

    > * {
      opacity: 0;
      .foot.is-visible & {
        animation: fade-up 0.85s $ease-soft both;
      }
    }

    > *:nth-child(1) { animation-delay: 0.20s; }
    > *:nth-child(2) { animation-delay: 0.30s; }
    > *:nth-child(3) { animation-delay: 0.40s; }
    > *:nth-child(4) { animation-delay: 0.50s; }
  }

  &__col {
    display: flex;
    flex-direction: column;
    gap: 16px;

    min-width: 0;
  }

  /* ---------------------------------------------------------------------
     Бренд
     --------------------------------------------------------------------- */

  &__mark {
    font-family: $serif;
    font-size: 1.875rem;
    font-weight: 700;
    letter-spacing: -0.03em;
    line-height: 1;
    color: $paper;
  }

  &__mark-dot {
    color: $accent;
    margin: 0 2px;
  }

  &__tagline {
    max-width: 38ch;
    margin: 0;

    font-family: $serif;
    font-size: 0.9375rem;
    line-height: 1.5;
    color: rgba(244, 236, 223, 0.62);
  }

  /* --- Бейджи статуса --- */

  .badges {
    list-style: none;
    margin: 4px 0 0;
    padding: 0;

    display: flex;
    flex-direction: column;
    gap: 8px;
  }

  .badges__item {
    display: inline-flex;
    align-items: center;
    gap: 10px;

    font-family: $mono;
    font-size: 0.625rem;
    letter-spacing: 0.16em;
    text-transform: uppercase;
    color: $muted;
  }

  .badges__dot {
    flex: none;

    width: 6px;
    height: 6px;
    border-radius: 50%;

    background-color: $accent;
    box-shadow: 0 0 0 3px rgba(200, 135, 74, 0.15);
  }

  /* ---------------------------------------------------------------------
     Лейбл колонки
     --------------------------------------------------------------------- */

  &__label {
    display: inline-flex;
    align-items: center;
    gap: 10px;

    font-family: $mono;
    font-size: 0.5625rem;
    font-weight: 600;
    letter-spacing: 0.28em;
    text-transform: uppercase;
    color: $muted-2;
  }

  &__label::before {
    content: "";
    width: 20px;
    height: 1px;
    background: $accent;
  }

  /* ---------------------------------------------------------------------
     Списки
     --------------------------------------------------------------------- */

  &__list {
    list-style: none;
    margin: 0;
    padding: 0;

    display: flex;
    flex-direction: column;

    li + li {
      border-top: 1px solid $hairline-2;
    }
  }

  &__link {
    display: grid;
    grid-template-columns: 1fr auto;
    align-items: baseline;
    gap: 12px;

    padding: 9px 0;

    font-family: $serif;
    font-size: 0.9375rem;
    font-weight: 400;
    letter-spacing: -0.005em;
    color: $paper;
    text-decoration: none;

    transition:
      color     0.25s $ease-soft,
      padding   0.25s $ease-soft;

    span {
      font-family: $mono;
      font-size: 0.5625rem;
      letter-spacing: 0.14em;
      color: $muted-2;

      transition: color 0.25s $ease-soft;
    }

    &:hover {
      color: $accent;
      padding-left: 4px;
    }

    &:hover span {
      color: $accent;
    }
  }

  /* --- Контакты — отдельный стиль строки --- */

  &__list--contacts li + li {
    border-top: 1px solid $hairline-2;
  }

  .contact {
    display: grid;
    grid-template-columns: 1fr auto;
    grid-template-rows: auto auto;
    align-items: center;
    gap: 0 12px;

    padding: 10px 0;

    color: inherit;
    text-decoration: none;

    transition: color 0.25s $ease-soft, padding 0.25s $ease-soft;
  }

  .contact__label {
    grid-column: 1 / 2;
    grid-row: 1 / 2;

    font-family: $mono;
    font-size: 0.5625rem;
    letter-spacing: 0.22em;
    text-transform: uppercase;
    color: $muted-2;
  }

  .contact__val {
    grid-column: 1 / 2;
    grid-row: 2 / 3;

    font-family: $serif;
    font-size: 1.0625rem;
    font-weight: 400;
    letter-spacing: -0.005em;
    color: $paper;
  }

  .contact__arrow {
    grid-column: 2 / 3;
    grid-row: 1 / 3;

    font-family: $mono;
    font-size: 0.9375rem;
    color: $muted-2;

    transition:
      color     0.25s $ease-soft,
      transform 0.3s $ease-soft;
  }

  .contact:hover {
    color: $accent;
    padding-left: 4px;
  }

  .contact:hover .contact__val { color: $accent; }

  .contact:hover .contact__arrow {
    color: $accent;
    transform: translate(3px, -3px);
  }

  /* ---------------------------------------------------------------------
     CTA
     --------------------------------------------------------------------- */

  .cta {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 18px;

    margin-top: 6px;
    padding: 14px 20px;

    background-color: $accent;
    color: #100a06;

    font-family: $mono;
    font-size: 0.6875rem;
    font-weight: 600;
    letter-spacing: 0.14em;
    text-transform: uppercase;
    text-decoration: none;

    border-radius: 2px;

    transition:
      background-color 0.3s $ease-soft,
      transform        0.3s $ease-soft,
      box-shadow       0.3s $ease-soft;

    &:hover {
      background-color: #d99b5e;
      transform: translateY(-1px);
      box-shadow: 0 16px 34px rgba(200, 135, 74, 0.28);
    }

    &:hover .cta__arrow {
      transform: translateX(5px);
    }
  }

  .cta__arrow {
    display: inline-block;
    font-size: 0.9375rem;
    letter-spacing: 0;

    transition: transform 0.3s $ease-soft;
  }

  /* ---------------------------------------------------------------------
     Нижняя полоса
     --------------------------------------------------------------------- */

  &__bottom {
    position: relative;
    z-index: 1;

    display: grid;
    grid-template-columns: 1fr auto 1fr;
    align-items: center;
    gap: 20px;

    font-family: $mono;
    font-size: 0.625rem;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: $muted-2;

    opacity: 0;
    .foot.is-visible & {
      animation: fade-in 0.9s $ease-soft 0.7s both;
    }
  }

  &__copy {
    justify-self: start;
    color: $muted;
  }

  &__legal {
    display: inline-flex;
    align-items: center;
    gap: 12px;

    justify-self: center;
  }

  &__legal-link {
    color: $muted-2;
    text-decoration: none;

    transition: color 0.25s $ease-soft;

    &:hover { color: $paper; }
  }

  &__legal-sep {
    color: $hairline;
  }

  &__legal-text {
    color: $muted-2;
  }

  /* --- Наверх --- */

  &__up {
    justify-self: end;

    display: inline-flex;
    align-items: center;
    gap: 8px;

    padding: 6px 10px;

    color: $muted;
    text-decoration: none;

    border: 1px solid $hairline;
    border-radius: 2px;

    transition:
      color        0.25s $ease-soft,
      border-color 0.25s $ease-soft,
      background-color 0.25s $ease-soft;

    &:hover {
      color: $paper;
      border-color: $accent;
      background-color: rgba(200, 135, 74, 0.10);
    }

    &:hover .foot__up-arrow {
      transform: translateY(-2px);
    }
  }

  &__up-label {
    font-family: $mono;
    font-size: 0.5625rem;
    letter-spacing: 0.24em;
    text-transform: uppercase;
  }

  &__up-arrow {
    font-family: $mono;
    font-size: 0.8125rem;
    color: $accent;

    transition: transform 0.3s $ease-soft;
  }
}

/* ==========================================================================
   АДАПТИВ
   ========================================================================== */

@media (max-width: 1180px) {
  .foot__grid {
    grid-template-columns: 1.5fr 1fr 1.3fr;
    gap: 32px;
  }

  .foot__col--nav:nth-of-type(3) {
    grid-column: 3 / 4;
    grid-row: 1 / 2;
  }

  .foot__col--contacts {
    grid-column: 1 / -1;
    padding-top: 20px;
    border-top: 1px solid $hairline;
  }
}

@media (max-width: 820px) {
  .foot {
    padding: 32px 5vw 18px;
  }

  .foot__kicker {
    padding-bottom: 12px;
    margin-bottom: 22px;
  }

  .foot__grid {
    grid-template-columns: 1fr;
    gap: 28px;
    padding-bottom: 24px;
    margin-bottom: 16px;
  }

  .foot__col--contacts {
    grid-column: auto;
    padding-top: 0;
    border-top: 0;
  }

  .foot__mark { font-size: 1.625rem; }

  .foot__tagline {
    max-width: 100%;
    font-size: 0.875rem;
  }

  .contact__val { font-size: 1rem; }

  .foot__bottom {
    grid-template-columns: 1fr;
    gap: 10px;
  }

  .foot__copy,
  .foot__legal,
  .foot__up {
    justify-self: start;
  }

  .foot__legal {
    flex-wrap: wrap;
    gap: 8px;
  }

  .foot__legal-sep { display: none; }

  .foot__legal-text {
    display: block;
    width: 100%;
  }
}
</style>