<!-- 7.vue -->
<template>
  <section ref="root" class="bots" :class="{ 'is-visible': visible }">
    <!-- Прозрачный чёрный блюр (стекло), без градиента -->
    <div class="bots__backdrop" aria-hidden="true"></div>

    <!-- Тонкая сетка -->
    <div class="bots__grid" aria-hidden="true"></div>

    <!-- ================================================================
         ШАПКА
         ================================================================ -->
    <header class="bots__head">
      <span class="bots__label">07 — Автоматизация</span>
      <h2 class="bots__title">Диалоги</h2>
      <span class="bots__meta">Issue 01 · MMXXVI</span>
    </header>

    <div class="bots__stage">
      <!-- ==============================================================
           СНОСКИ: в полях по бокам сцены
           ============================================================== -->
      <div class="anno anno--db">
        <span class="anno__dot"></span>
        <span class="anno__line"></span>
        <span class="anno__text">
          <b>Одна база</b>
          <em>Заявки из Telegram и VK стекаются в одно окно.</em>
        </span>
      </div>

      <div class="anno anno--control">
        <span class="anno__dot"></span>
        <span class="anno__line"></span>
        <span class="anno__text">
          <b>Управление</b>
          <em>Включить, пауза, аналитика — в один клик.</em>
        </span>
      </div>

      <div class="anno anno--context">
        <span class="anno__dot"></span>
        <span class="anno__line"></span>
        <span class="anno__text">
          <b>Контекст</b>
          <em>Бот помнит, что вы обсуждали, и не теряет заявку.</em>
        </span>
      </div>

      <div class="anno anno--speed">
        <span class="anno__dot"></span>
        <span class="anno__line"></span>
        <span class="anno__text">
          <b>~2 сек</b>
          <em>Средний ответ. Диалог не остывает ни днём, ни ночью.</em>
        </span>
      </div>

      <!-- ==============================================================
           ЛЕВО — МАСТХЕД
           ============================================================== -->
      <div class="masthead">
        <span class="masthead__kicker">Всего диалогов</span>
        <span class="masthead__num">550</span>
        <span class="masthead__unit">Q1 · MMXXVI</span>

        <span class="masthead__rule" aria-hidden="true"></span>

        <ul class="masthead__index">
          <li>
            <span class="idx">01</span>
            <span class="k">Заявок</span>
            <span class="v">278</span>
          </li>
          <li>
            <span class="idx">02</span>
            <span class="k">Конверсия</span>
            <span class="v">51<em>%</em></span>
          </li>
          <li>
            <span class="idx">03</span>
            <span class="k">Ответ</span>
            <span class="v">~2<em>с</em></span>
          </li>
        </ul>

        <span class="masthead__foot">
          Автоматические ответы в двух каналах
        </span>
      </div>

      <!-- ==============================================================
           ЦЕНТР — ТЕЛЕФОН С ЧАТОМ БОТА
           ============================================================== -->
      <div class="phone-wrap">
        <div class="phone">
          <div class="phone__screen">
            <div class="phone__notch"></div>

            <header class="chat-head">
              <span class="chat-head__avatar" aria-hidden="true">
                <svg viewBox="0 0 40 40" width="100%" height="100%">
                  <rect width="40" height="40" fill="#c8874a"/>
                  <circle cx="20" cy="15" r="7" fill="#ede0c8"/>
                  <path d="M6 40c2-9 8-13 14-13s12 4 14 13z" fill="#ede0c8"/>
                </svg>
              </span>

              <div class="chat-head__body">
                <span class="chat-head__name">Лофт «Кадр» · Бот</span>
                <span class="chat-head__status">
                  <em></em> online · отвечает быстро
                </span>
              </div>

              <span class="chat-head__back" aria-hidden="true">‹</span>
            </header>

            <div class="chat-body">
              <span class="chat-day">Сегодня · 12:24</span>

              <div class="msg msg--in">
                <p>Здравствуйте, Анна! 👋</p>
                <span class="msg__time">12:24</span>
              </div>

              <div class="msg msg--in msg--wide">
                <p>Выберите зал для съёмки:</p>
                <div class="msg__chips">
                  <span class="chip chip--active">B2 · студия</span>
                  <span class="chip">B1 · лофт</span>
                  <span class="chip">A1 · зал</span>
                </div>
                <span class="msg__time">12:24</span>
              </div>

              <div class="msg msg--out">
                <p>B2, 13 Пн, 12:30</p>
                <span class="msg__time">12:25 ✓✓</span>
              </div>

              <div class="msg msg--in msg--wide">
                <p>
                  <b>✓ Заявка принята.</b><br>
                  Ждём вас 13 мая в 12:30.
                </p>
                <div class="msg__chips">
                  <span class="chip chip--ok">Подтвердить</span>
                  <span class="chip chip--ghost">Изменить</span>
                </div>
                <span class="msg__time">12:25</span>
              </div>

              <div class="msg msg--in msg--typing">
                <span class="dot"></span>
                <span class="dot"></span>
                <span class="dot"></span>
              </div>
            </div>

            <footer class="chat-input">
              <span class="chat-input__field">Написать сообщение…</span>
              <span class="chat-input__send" aria-hidden="true">→</span>
            </footer>
          </div>
        </div>
      </div>

      <!-- ==============================================================
           ПРАВО — ДВЕ КАРТОЧКИ КАНАЛОВ
           ============================================================== -->
      <div class="cards">
        <article class="bot bot--tg">
          <header class="bot__head">
            <span class="bot__idx">01</span>
            <span class="bot__name">Telegram</span>
          </header>

          <div class="bot__row">
            <div class="bot__badge" aria-hidden="true">
              <svg viewBox="0 0 24 24" width="18" height="18">
                <path fill="currentColor" d="M21.8 4.3 2.9 11.6c-.9.3-.9 1.5.1 1.8l4.5 1.4 1.7 5.2c.2.7 1.2.8 1.6.2l2.4-2.6 4.6 3.4c.6.4 1.4.1 1.6-.6l2.7-15.3c.2-.9-.8-1.6-1.6-1.2zM9.1 14.6l9.4-6.4-7.6 7.5-.2 3.5-1.6-4.6z" />
              </svg>
            </div>
            <span class="bot__handle">@loftkadr_bot</span>
          </div>

          <dl class="bot__stats">
            <div class="stat">
              <dt>Диалогов</dt>
              <dd>340</dd>
            </div>
            <div class="stat">
              <dt>Заявок</dt>
              <dd>182</dd>
            </div>
            <div class="stat stat--hl">
              <dt>Конверсия</dt>
              <dd>53<em>%</em></dd>
            </div>
          </dl>

          <div class="bot__bar" aria-hidden="true">
            <span style="--w: 53%"></span>
          </div>
        </article>

        <article class="bot bot--vk">
          <header class="bot__head">
            <span class="bot__idx">02</span>
            <span class="bot__name">VK</span>
          </header>

          <div class="bot__row">
            <div class="bot__badge" aria-hidden="true">
              <svg viewBox="0 0 24 24" width="18" height="18">
                <path fill="currentColor" d="M12.8 16.4h1.3c.4 0 .5-.3.5-.6 0-.9.6-1.1 1.3-.4 1.2 1.1 2.3 1.1 2.9 1.1h1.6c.5 0 .7-.3.5-.8-.2-.5-.9-1.4-1.8-2.4-.7-.8-.7-1.2 0-2 .5-.6 1.5-1.7 1.8-2.3.3-.5.1-.8-.5-.8h-1.6c-.5 0-.7.3-.9.7-.2.6-.7 1.7-1.4 2.5-.6.7-1 .8-1.2.8-.2 0-.4-.2-.4-.8V9.1c0-.6-.1-.8-.5-.8h-2.6c-.3 0-.5.2-.5.5 0 .5.7.6.8 1.6v2.4c0 .7-.1.8-.3.8-.4 0-1-.5-1.6-1.4-.8-1.1-1.3-2.4-1.5-3-.2-.4-.4-.6-.9-.6H5.3c-.5 0-.7.2-.6.7.2 1 .8 2.5 2 4.1 1.4 1.9 3.2 2.9 5 2.9z M13 11.5v-.1z" />
              </svg>
            </div>
            <span class="bot__handle">vk.me/loftkadr</span>
          </div>

          <dl class="bot__stats">
            <div class="stat">
              <dt>Диалогов</dt>
              <dd>210</dd>
            </div>
            <div class="stat">
              <dt>Заявок</dt>
              <dd>96</dd>
            </div>
            <div class="stat stat--hl">
              <dt>Конверсия</dt>
              <dd>46<em>%</em></dd>
            </div>
          </dl>

          <div class="bot__bar" aria-hidden="true">
            <span style="--w: 46%"></span>
          </div>
        </article>
      </div>
    </div>

    <!-- ================================================================
         ПОДПИСЬ
         ================================================================ -->
    <footer class="bots__sign">
      <span class="bots__sign-name">Лофт «Кадр»</span>
      <span class="bots__sign-line">Автоматизация · 2026</span>
    </footer>
  </section>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue'

/**
 * 7.vue — седьмой блок.
 *
 * Журнальный разворот про ботов в Telegram и VK.
 *
 * Фон: прозрачный чёрный блюр (стекло), без градиента.
 * Сноски: в боковых полях сцены (только на десктопе).
 * Центр: макет телефона с чатом бота.
 *
 * Мобильная версия:
 *  · мастхед (гигантская цифра) скрыт;
 *  · сноски скрыты;
 *  · телефон крупный по центру;
 *  · карточки каналов ужаты.
 *
 * Палитра — кофейная. Анимации ленивые, через IntersectionObserver.
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
        if (entry.isIntersecting && entry.intersectionRatio >= 0.3) {
          if (visible.value) return
          await nextTick()
          visible.value = true
        } else if (!entry.isIntersecting) {
          visible.value = false
        }
      }
    },
    { threshold: [0, 0.3, 0.6] }
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
$muted:       rgba(244, 236, 223, 0.62);
$muted-2:     rgba(244, 236, 223, 0.42);

$paper:       #ede0c8;
$paper-deep:  #d9c7a6;

$ink:         #1a1108;
$ink-soft:    rgba(26, 17, 8, 0.62);

$accent:      #c8874a;
$accent-soft: #e0b78a;
$accent-deep: #8a5a2c;

$espresso:    #100a06;
$espresso-2:  #1a120c;

$faint:       rgba(200, 170, 135, 0.10);
$rule:        rgba(200, 170, 135, 0.22);
$rule-strong: rgba(200, 170, 135, 0.38);

$pad-x:     clamp(140px, 14vw, 220px);
$pad-t:     4vh;
$pad-b:     5vh;

$mono: "IBM Plex Mono", "JetBrains Mono", ui-monospace,
       SFMono-Regular, Menlo, Consolas, monospace;

$serif: Georgia, "Times New Roman", serif;

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

@keyframes rise {
  from { opacity: 0; transform: translateY(18px); }
  to   { opacity: 1; transform: translateY(0);    }
}

@keyframes number-in {
  from { opacity: 0; transform: translateY(24px) scale(0.96); letter-spacing: -0.02em; }
  to   { opacity: 1; transform: translateY(0)    scale(1);    letter-spacing: -0.06em; }
}

@keyframes bar-grow {
  from { transform: scaleX(0); }
  to   { transform: scaleX(1); }
}

@keyframes rule-grow {
  from { transform: scaleX(0); }
  to   { transform: scaleX(1); }
}

@keyframes msg-in {
  from { opacity: 0; transform: translateY(8px) scale(0.98); }
  to   { opacity: 1; transform: translateY(0)   scale(1);    }
}

@keyframes dot-pulse {
  0%, 60%, 100% { opacity: 0.35; transform: translateY(0); }
  30%           { opacity: 1;    transform: translateY(-2px); }
}

/* ==========================================================================
   БЛОК
   ========================================================================== */

.bots {
  position: relative;

  display: flex;
  flex-direction: column;

  width: 100%;
  height: 100%;

  min-height: 0;
  box-sizing: border-box;

  padding: $pad-t $pad-x $pad-b;

  color: $text;

  overflow: hidden;

  &__backdrop {
    position: absolute;
    inset: 0;

    background-color: rgba(0, 0, 0, 0.28);

    backdrop-filter: blur(40px) saturate(110%);
    -webkit-backdrop-filter: blur(40px) saturate(110%);

    pointer-events: none;
    z-index: 0;

    opacity: 0;
    .bots.is-visible & {
      animation: fade-in 1.2s $ease-soft 0.05s both;
    }
  }

  &__grid {
    position: absolute;
    inset: 0;

    background-image:
      linear-gradient(to right, $faint 1px, transparent 1px),
      linear-gradient(to bottom, $faint 1px, transparent 1px);
    background-size: 88px 88px;
    background-position: $pad-x $pad-t;

    mask-image: radial-gradient(120% 90% at 50% 50%, #000 40%, transparent 100%);
    -webkit-mask-image: radial-gradient(120% 90% at 50% 50%, #000 40%, transparent 100%);

    pointer-events: none;
    z-index: 0;

    opacity: 0;
    .bots.is-visible & {
      animation: fade-in 1.6s $ease-soft 0.15s both;
    }
  }

  &__head {
    position: relative;
    z-index: 5;

    display: grid;
    grid-template-columns: 1fr auto;
    align-items: end;

    gap: 8px;

    flex: 0 0 auto;
    margin-bottom: 3vh;

    > * { opacity: 0; }

    .bots.is-visible & > * {
      animation: fade-down 0.9s $ease-soft both;
    }
    .bots.is-visible & > *:nth-child(1) { animation-delay: 0.10s; }
    .bots.is-visible & > *:nth-child(2) { animation-delay: 0.22s; }
    .bots.is-visible & > *:nth-child(3) { animation-delay: 0.34s; }
  }

  &__label,
  &__sign-name,
  &__sign-line {
    font-family: $mono;
    font-size: 0.6875rem;
    font-weight: 600;
    letter-spacing: 0.28em;
    text-transform: uppercase;
  }

  &__label { color: $muted; }

  &__title {
    font-family: $serif;
    font-size: clamp(2rem, 3.4vw, 2.75rem);
    font-weight: 400;
    letter-spacing: -0.02em;
    line-height: 1;
    color: $paper;

    grid-column: 1 / 2;
  }

  &__meta {
    grid-column: 2 / 3;
    grid-row: 1 / 3;
    align-self: start;

    font-family: $mono;
    font-size: 0.6875rem;
    letter-spacing: 0.22em;
    text-transform: uppercase;
    color: $muted;
  }

  &__stage {
    position: relative;
    z-index: 2;

    flex: 1 1 auto;
    min-height: 0;

    display: grid;
    grid-template-columns: 1.05fr 0.9fr 1fr;
    gap: clamp(16px, 2vw, 28px);
    align-items: stretch;
  }

  &__sign {
    position: absolute;
    right: $pad-x;
    bottom: $pad-b;

    display: flex;
    flex-direction: column;
    align-items: flex-end;
    gap: 2px;

    text-align: right;

    z-index: 5;
    pointer-events: none;

    opacity: 0;
    .bots.is-visible & {
      animation: fade-in 1s $ease-soft 1.6s both;
    }

    &-name { color: $text; }
    &-line { color: $muted; }
  }
}

/* ==========================================================================
   СНОСКИ
   ========================================================================== */

.anno {
  position: absolute;

  display: flex;
  align-items: flex-start;
  gap: 10px;

  max-width: calc(#{$pad-x} - 40px);

  z-index: 8;
  pointer-events: none;

  opacity: 0;

  .bots.is-visible & {
    animation: fade-in 0.8s $ease-soft both;
  }

  &__dot {
    flex: none;

    width: 7px;
    height: 7px;
    margin-top: 4px;

    border-radius: 50%;

    background-color: $accent;
    box-shadow:
      0 0 0 3px rgba(200, 135, 74, 0.20),
      0 0 12px rgba(200, 135, 74, 0.55);
  }

  &__line {
    flex: none;

    width: 28px;
    height: 1px;
    margin-top: 7px;

    background-color: $text;
    opacity: 0.55;
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

      color: $accent-soft;
      text-shadow: 0 1px 6px rgba(0, 0, 0, 0.6);
    }

    em {
      font-family: $serif;
      font-style: italic;
      font-size: 0.75rem;
      font-weight: 400;
      letter-spacing: 0.005em;
      line-height: 1.4;

      color: rgba(244, 236, 223, 0.88);
      text-shadow: 0 1px 6px rgba(0, 0, 0, 0.55);
    }
  }
}

.anno--db {
  top: 6%;
  left: calc(-1 * #{$pad-x} + 24px);

  flex-direction: row-reverse;

  .anno__text {
    align-items: flex-end;
    text-align: right;
  }

  .bots.is-visible & { animation-delay: 0.45s; }
}

.anno--context {
  bottom: 6%;
  left: calc(-1 * #{$pad-x} + 24px);

  flex-direction: row-reverse;

  .anno__text {
    align-items: flex-end;
    text-align: right;
  }

  .bots.is-visible & { animation-delay: 0.75s; }
}

.anno--control {
  top: 6%;
  right: calc(-1 * #{$pad-x} + 24px);

  .bots.is-visible & { animation-delay: 0.6s; }
}

.anno--speed {
  bottom: 6%;
  right: calc(-1 * #{$pad-x} + 24px);

  .bots.is-visible & { animation-delay: 0.9s; }
}

/* ==========================================================================
   МАСТХЕД
   ========================================================================== */

.masthead {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;

  padding: clamp(20px, 2.4vw, 32px);

  background: linear-gradient(
    180deg,
    rgba(255, 255, 255, 0.035) 0%,
    rgba(255, 255, 255, 0.01) 100%
  );
  border: 1px solid $rule;
  border-radius: 3px;

  position: relative;
  overflow: hidden;

  opacity: 0;
  .bots.is-visible & {
    animation: rise 1s $ease-soft 0.35s both;
  }

  &__kicker {
    font-family: $mono;
    font-size: 0.6875rem;
    font-weight: 600;
    letter-spacing: 0.32em;
    text-transform: uppercase;
    color: $accent-soft;
    margin-bottom: 10px;
  }

  &__num {
    display: block;

    font-family: $serif;
    font-size: clamp(5rem, 10vw, 10rem);
    font-weight: 700;
    letter-spacing: -0.06em;
    line-height: 0.82;

    color: $paper;

    text-shadow: 0 6px 40px rgba(200, 135, 74, 0.28);

    opacity: 0;
    .bots.is-visible & {
      animation: number-in 1.2s $ease-soft 0.5s both;
    }
  }

  &__unit {
    margin-top: 6px;

    font-family: $mono;
    font-size: 0.75rem;
    letter-spacing: 0.24em;
    text-transform: uppercase;
    color: $muted;
  }

  &__rule {
    display: block;
    height: 1px;
    width: 100%;

    margin: clamp(16px, 2.2vh, 28px) 0;

    background: linear-gradient(
      to right,
      $rule-strong 0%,
      $rule 40%,
      transparent 100%
    );

    transform-origin: left center;
    .bots.is-visible & {
      animation: rule-grow 1s $ease-soft 0.9s both;
    }
  }

  &__index {
    list-style: none;
    margin: 0;
    padding: 0;

    display: flex;
    flex-direction: column;
    gap: 10px;

    li {
      display: grid;
      grid-template-columns: 32px 1fr auto;
      align-items: baseline;
      gap: 12px;

      opacity: 0;
      .bots.is-visible & {
        animation: fade-in 0.8s $ease-soft both;
      }
    }

    li:nth-child(1) { animation-delay: 1.0s; }
    li:nth-child(2) { animation-delay: 1.1s; }
    li:nth-child(3) { animation-delay: 1.2s; }

    .idx {
      font-family: $mono;
      font-size: 0.625rem;
      font-weight: 700;
      letter-spacing: 0.2em;
      color: $accent;
    }

    .k {
      font-family: $mono;
      font-size: 0.6875rem;
      letter-spacing: 0.22em;
      text-transform: uppercase;
      color: $muted;
    }

    .v {
      font-family: $serif;
      font-size: 1.5rem;
      font-weight: 700;
      letter-spacing: -0.01em;
      color: $paper;

      em {
        font-family: $mono;
        font-size: 0.75rem;
        font-style: normal;
        font-weight: 500;
        color: $muted;
        margin-left: 2px;
      }
    }
  }

  &__foot {
    margin-top: auto;
    padding-top: clamp(16px, 2.4vh, 28px);

    font-family: $mono;
    font-size: 0.625rem;
    letter-spacing: 0.24em;
    text-transform: uppercase;
    color: $muted-2;
  }
}

/* ==========================================================================
   ТЕЛЕФОН
   ========================================================================== */

.phone-wrap {
  display: flex;
  align-items: center;
  justify-content: center;

  min-height: 0;

  opacity: 0;
  .bots.is-visible & {
    animation: rise 1.1s $ease-soft 0.55s both;
  }
}

.phone {
  height: 100%;
  max-height: 100%;

  aspect-ratio: 9 / 17;

  max-width: 100%;

  &__screen {
    position: relative;

    width: 100%;
    height: 100%;

    background-color: $espresso;
    border: 8px solid #060403;
    border-radius: 38px;

    box-shadow:
      0 36px 72px rgba(0, 0, 0, 0.65),
      0 0 0 1px rgba(255, 255, 255, 0.06) inset;

    overflow: hidden;

    display: flex;
    flex-direction: column;
  }

  &__notch {
    position: absolute;
    top: 8px;
    left: 50%;
    transform: translateX(-50%);

    width: 64px;
    height: 18px;

    background-color: #060403;
    border-radius: 999px;

    z-index: 4;
  }
}

.chat-head {
  flex: 0 0 auto;

  display: flex;
  align-items: center;
  gap: 10px;

  padding: 26px 12px 10px;

  background-color: $espresso-2;
  border-bottom: 1px solid rgba(200, 170, 135, 0.14);

  &__avatar {
    flex: none;

    width: 32px;
    height: 32px;

    border-radius: 50%;
    overflow: hidden;

    border: 1.5px solid rgba(200, 135, 74, 0.55);
  }

  &__body {
    display: flex;
    flex-direction: column;
    gap: 1px;

    flex: 1;
    min-width: 0;
  }

  &__name {
    font-family: $serif;
    font-size: 0.8125rem;
    font-weight: 700;
    color: $paper;

    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  &__status {
    display: flex;
    align-items: center;
    gap: 5px;

    font-family: $mono;
    font-size: 0.5rem;
    letter-spacing: 0.14em;
    text-transform: uppercase;
    color: $muted;

    em {
      display: inline-block;

      width: 5px;
      height: 5px;

      border-radius: 50%;
      background-color: #7db571;

      box-shadow: 0 0 6px rgba(125, 181, 113, 0.7);
    }
  }

  &__back {
    flex: none;

    font-family: $mono;
    font-size: 1.1rem;
    color: $muted;
    line-height: 1;

    padding: 0 2px;
  }
}

.chat-body {
  flex: 1 1 auto;
  min-height: 0;

  display: flex;
  flex-direction: column;
  gap: 8px;

  padding: 12px 10px;

  background:
    radial-gradient(120% 70% at 50% 0%, rgba(200, 135, 74, 0.08) 0%, transparent 55%),
    linear-gradient(180deg, $espresso 0%, $espresso-2 100%);

  overflow-y: auto;
  overscroll-behavior: contain;
  -webkit-overflow-scrolling: touch;

  scrollbar-width: none;
  &::-webkit-scrollbar { display: none; }
}

.chat-day {
  align-self: center;

  padding: 3px 10px;
  margin-bottom: 2px;

  font-family: $mono;
  font-size: 0.5rem;
  letter-spacing: 0.16em;
  text-transform: uppercase;

  color: $muted;
  background-color: rgba(255, 255, 255, 0.05);
  border-radius: 999px;
}

.msg {
  position: relative;

  max-width: 84%;
  padding: 8px 11px 16px;

  font-family: $serif;
  font-size: 0.75rem;
  line-height: 1.35;

  border-radius: 12px;

  opacity: 0;
  .bots.is-visible & {
    animation: msg-in 0.5s $ease-soft both;
  }

  p {
    margin: 0;
    color: inherit;
  }

  b { font-weight: 700; }

  &__time {
    position: absolute;
    right: 8px;
    bottom: 4px;

    font-family: $mono;
    font-size: 0.4375rem;
    letter-spacing: 0.05em;

    opacity: 0.6;
  }

  &--in {
    align-self: flex-start;

    background-color: $paper;
    color: $ink;

    border-bottom-left-radius: 4px;
  }

  &--out {
    align-self: flex-end;

    background-color: $accent;
    color: $espresso;

    border-bottom-right-radius: 4px;
  }

  &--wide {
    max-width: 92%;
  }

  &:nth-of-type(1) { animation-delay: 0.75s; }
  &:nth-of-type(2) { animation-delay: 0.95s; }
  &:nth-of-type(3) { animation-delay: 1.15s; }
  &:nth-of-type(4) { animation-delay: 1.35s; }

  &--typing {
    display: flex;
    align-items: center;
    gap: 4px;

    padding: 9px 11px;

    background-color: $paper;

    animation-delay: 1.55s;

    .dot {
      width: 5px;
      height: 5px;

      border-radius: 50%;
      background-color: rgba(26, 17, 8, 0.55);

      animation: dot-pulse 1.2s infinite ease-in-out;
    }
    .dot:nth-child(2) { animation-delay: 0.15s; }
    .dot:nth-child(3) { animation-delay: 0.3s; }
  }

  &__chips {
    display: flex;
    flex-wrap: wrap;
    gap: 4px;

    margin-top: 6px;
  }
}

.chip {
  display: inline-block;

  padding: 4px 9px;

  font-family: $mono;
  font-size: 0.5rem;
  font-weight: 600;
  letter-spacing: 0.06em;
  text-transform: uppercase;

  color: $ink;
  background-color: rgba(26, 17, 8, 0.08);
  border: 1px solid rgba(26, 17, 8, 0.12);
  border-radius: 999px;

  white-space: nowrap;

  &--active {
    background-color: $accent-deep;
    color: $paper;
    border-color: $accent-deep;
  }

  &--ok {
    background-color: #6b8f4a;
    color: $paper;
    border-color: #6b8f4a;
  }

  &--ghost {
    background-color: transparent;
    color: $ink-soft;
  }
}

.chat-input {
  flex: 0 0 auto;

  display: flex;
  align-items: center;
  gap: 8px;

  padding: 8px 10px 12px;

  background-color: $espresso-2;
  border-top: 1px solid rgba(200, 170, 135, 0.14);

  &__field {
    flex: 1;
    min-width: 0;

    padding: 7px 12px;

    font-family: $serif;
    font-size: 0.6875rem;
    color: $muted;

    background-color: rgba(255, 255, 255, 0.05);
    border-radius: 999px;

    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  &__send {
    flex: none;

    display: grid;
    place-items: center;

    width: 28px;
    height: 28px;

    font-family: $mono;
    font-size: 0.875rem;
    font-weight: 700;

    color: $espresso;
    background-color: $accent;
    border-radius: 50%;
  }
}

/* ==========================================================================
   КАРТОЧКИ КАНАЛОВ
   ========================================================================== */

.cards {
  display: grid;
  grid-template-rows: 1fr 1fr;
  gap: clamp(12px, 1.4vw, 20px);
  min-height: 0;
}

.bot {
  display: flex;
  flex-direction: column;

  padding: clamp(14px, 1.6vw, 20px);

  background: linear-gradient(
    180deg,
    rgba(255, 255, 255, 0.035) 0%,
    rgba(255, 255, 255, 0.01) 100%
  );
  border: 1px solid $rule;
  border-radius: 3px;

  position: relative;

  min-height: 0;

  opacity: 0;
  .bots.is-visible & {
    animation: rise 1s $ease-soft both;
  }
  .bots.is-visible &--tg { animation-delay: 0.75s; }
  .bots.is-visible &--vk { animation-delay: 0.9s; }

  &__head {
    display: flex;
    align-items: baseline;
    gap: 12px;

    margin-bottom: 12px;
    padding-bottom: 10px;

    border-bottom: 1px solid $rule;
  }

  &__idx {
    font-family: $mono;
    font-size: 0.5625rem;
    font-weight: 700;
    letter-spacing: 0.22em;
    color: $accent;
  }

  &__name {
    font-family: $mono;
    font-size: 0.75rem;
    font-weight: 600;
    letter-spacing: 0.28em;
    text-transform: uppercase;
    color: $paper;
  }

  &__row {
    display: flex;
    align-items: center;
    gap: 10px;

    margin-bottom: 12px;
  }

  &__badge {
    flex: none;

    display: grid;
    place-items: center;

    width: 32px;
    height: 32px;

    background-color: rgba(200, 135, 74, 0.12);
    border: 1px solid rgba(200, 135, 74, 0.28);
    border-radius: 4px;

    color: $accent-soft;
  }

  &--tg &__badge {
    background-color: rgba(80, 140, 200, 0.14);
    border-color: rgba(120, 170, 220, 0.32);
    color: #b6d2e6;
  }

  &--vk &__badge {
    background-color: rgba(80, 120, 170, 0.14);
    border-color: rgba(120, 150, 200, 0.32);
    color: #b6c4dc;
  }

  &__handle {
    font-family: $mono;
    font-size: 0.6875rem;
    letter-spacing: 0.12em;
    color: $muted;

    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  &__stats {
    margin: 0 0 12px;
    padding: 0;

    display: flex;
    flex-direction: column;
    gap: 6px;
  }

  .stat {
    display: grid;
    grid-template-columns: 1fr auto;
    align-items: baseline;
    gap: 10px;

    padding-bottom: 6px;
    border-bottom: 1px dashed rgba(200, 170, 135, 0.14);
  }

  .stat:last-child { border-bottom: 0; padding-bottom: 0; }

  .stat dt {
    font-family: $mono;
    font-size: 0.5625rem;
    letter-spacing: 0.22em;
    text-transform: uppercase;
    color: $muted;
  }

  .stat dd {
    margin: 0;

    font-family: $serif;
    font-size: 1.25rem;
    font-weight: 700;
    letter-spacing: -0.01em;
    color: $paper;

    em {
      font-family: $mono;
      font-size: 0.6875rem;
      font-style: normal;
      font-weight: 500;
      color: $muted;
      margin-left: 2px;
    }
  }

  .stat--hl dt { color: $accent; }
  .stat--hl dd {
    color: $accent-soft;
    text-shadow: 0 2px 14px rgba(200, 135, 74, 0.3);
  }

  &__bar {
    position: relative;

    height: 3px;
    margin-top: auto;

    background-color: rgba(200, 170, 135, 0.12);
    border-radius: 2px;

    overflow: hidden;

    span {
      position: absolute;
      inset: 0;

      width: var(--w, 50%);
      height: 100%;

      background: linear-gradient(to right, $accent-deep 0%, $accent 100%);
      border-radius: 2px;

      transform-origin: left center;
      .bots.is-visible & {
        animation: bar-grow 1.4s $ease-soft 1.4s both;
      }
    }
  }

  &--tg &__bar span {
    background: linear-gradient(to right, #4d7ba8 0%, #84b1d6 100%);
  }

  &--vk &__bar span {
    background: linear-gradient(to right, #466ea0 0%, #8faed0 100%);
  }
}

/* ==========================================================================
   ПЛАНШЕТ
   ========================================================================== */

@media (max-width: 1200px) {
  .bots {
    padding-left: 5vw;
    padding-right: 5vw;
  }

  .anno { display: none !important; }

  .bots__stage {
    grid-template-columns: 1fr 1fr;
    grid-template-areas:
      "masthead phone"
      "cards    cards";
  }

  .masthead    { grid-area: masthead; }
  .phone-wrap  { grid-area: phone; }
  .cards       { grid-area: cards; grid-template-columns: 1fr 1fr; grid-template-rows: 1fr; }

  .phone {
    aspect-ratio: 9 / 16;
  }

  .masthead__num {
    font-size: clamp(5rem, 14vw, 9rem);
  }
}

/* ==========================================================================
   МОБИЛЬНАЯ ВЕРСИЯ
   Мастхед вырезан, телефон крупный по центру, карточки ужаты
   ========================================================================== */

@media (max-width: 820px) {
  .bots {
    padding: 4vh 5vw;

    overflow-y: auto;
    overscroll-behavior: auto;
    -webkit-overflow-scrolling: touch;

    scrollbar-width: none;
    &::-webkit-scrollbar { display: none; }
  }

  .bots__head {
    margin-bottom: 2.5vh;
  }

  .bots__title {
    font-size: 1.75rem;
  }

  .bots__label,
  .bots__meta {
    font-size: 0.5625rem;
    letter-spacing: 0.2em;
  }

  /* Мастхед (цифра 550) полностью убираем */
  .masthead { display: none !important; }

  /* Сноски тоже */
  .anno { display: none !important; }

  /* Сцена: только телефон и карточки */
  .bots__stage {
    grid-template-columns: 1fr;
    grid-template-areas:
      "phone"
      "cards";
    gap: 18px;
  }

  .phone-wrap {
    grid-area: phone;
    padding: 4px 0 8px;
  }

  /* --- Телефон крупнее и по центру --- */
  .phone {
    height: auto;
    width: min(320px, 84vw);
    aspect-ratio: 9 / 17;
    margin: 0 auto;
  }

  .phone__screen {
    border-width: 7px;
    border-radius: 32px;
  }

  .phone__notch {
    width: 58px;
    height: 16px;
    top: 7px;
  }

  /* Чат — компактнее */
  .chat-head { padding: 24px 12px 10px; gap: 9px; }
  .chat-head__avatar { width: 30px; height: 30px; }
  .chat-head__name { font-size: 0.8125rem; }
  .chat-head__status { font-size: 0.5rem; letter-spacing: 0.12em; }

  .chat-body { padding: 12px 10px; gap: 8px; }

  .msg {
    font-size: 0.75rem;
    padding: 8px 11px 16px;
  }

  .msg__time { font-size: 0.4375rem; }

  .chip {
    font-size: 0.5rem;
    padding: 4px 9px;
  }

  .chat-input { padding: 8px 10px 12px; gap: 8px; }
  .chat-input__field { font-size: 0.6875rem; padding: 7px 12px; }
  .chat-input__send { width: 28px; height: 28px; font-size: 0.875rem; }

  /* --- Карточки: две в ряд, компактные --- */
  .cards {
    grid-area: cards;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: auto;
    gap: 10px;
  }

  .bot {
    padding: 12px;
  }

  .bot__head {
    margin-bottom: 10px;
    padding-bottom: 8px;
    gap: 8px;
  }

  .bot__name { font-size: 0.6875rem; letter-spacing: 0.22em; }
  .bot__idx { font-size: 0.5rem; }

  .bot__row {
    gap: 8px;
    margin-bottom: 10px;
  }

  .bot__badge { width: 26px; height: 26px; }
  .bot__handle { font-size: 0.5625rem; letter-spacing: 0.08em; }

  .bot__stats {
    gap: 4px;
    margin-bottom: 10px;
  }

  .bot .stat {
    padding-bottom: 4px;
    gap: 6px;
  }

  .bot .stat dt { font-size: 0.5rem; letter-spacing: 0.16em; }
  .bot .stat dd { font-size: 0.9375rem; }
  .bot .stat dd em { font-size: 0.5625rem; }

  /* --- Подпись --- */
  .bots__sign {
    position: static;
    margin-top: 20px;
    padding-top: 12px;

    align-items: flex-start;
    text-align: left;

    border-top: 1px solid $rule;
  }
}

@media (max-width: 400px) {
  .phone { width: min(280px, 88vw); }

  .bots__title { font-size: 1.5rem; }

  .bot { padding: 10px; }
  .bot__name { font-size: 0.625rem; letter-spacing: 0.18em; }
  .bot .stat dt { font-size: 0.4375rem; }
  .bot .stat dd { font-size: 0.875rem; }
}
</style>