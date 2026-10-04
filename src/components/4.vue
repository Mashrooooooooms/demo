<!-- 4.vue -->
<template>
  <section ref="root" class="cabinet" :class="{ 'is-visible': visible }">
    <div class="cabinet__backdrop" aria-hidden="true"></div>

    <header class="cabinet__head">
      <span class="cabinet__label">04 — Кабинет</span>
      <h2 class="cabinet__title">Заявки</h2>
      <span class="cabinet__meta">CLIENT → ADMIN · 01</span>
    </header>

    <!-- Мобильный тоглер: только на узких экранах -->
    <div class="cabinet__toggle" role="tablist">
      <button
        class="cabinet__toggle-btn"
        :class="{ 'is-active': mobileSide === 'client' }"
        role="tab"
        @click="mobileSide = 'client'"
      >
        <span class="cabinet__toggle-num">01</span>
        <span>Клиент</span>
      </button>
      <button
        class="cabinet__toggle-btn"
        :class="{ 'is-active': mobileSide === 'admin' }"
        role="tab"
        @click="mobileSide = 'admin'"
      >
        <span class="cabinet__toggle-num">02</span>
        <span>Админ</span>
      </button>
    </div>

    <div class="cabinet__stage">
      <!-- ЛЕВО: КЛИЕНТ -->
      <div
        class="side side--client"
        :class="{ 'is-hidden-mobile': mobileSide !== 'client' }"
      >
        <div class="side__head">
          <span class="side__num">01</span>
          <span class="side__name">Клиент</span>
        </div>

        <div class="composition">
          <div class="monitor">
            <div class="monitor__screen">
              <div class="monitor__bar">
                <span></span><span></span><span></span>
                <em>loft-kadr.app / new-request</em>
              </div>

              <div class="monitor__content monitor__content--client">
                <div class="dash__hero">
                  <img src="/portret.jpg" alt="">
                  <div class="dash__hero-copy">
                    <span class="dash__kicker">Новая заявка</span>
                    <span class="dash__title">Фотосессия</span>
                  </div>
                </div>

                <div class="dash__form">
                  <div class="fld">
                    <label>Имя</label>
                    <input
                      v-model="clientForm.name"
                      class="inline-input"
                      type="text"
                      maxlength="24"
                    >
                  </div>

                  <div class="fld">
                    <label>Зал</label>
                    <span>{{ clientForm.room }}</span>
                  </div>

                  <div class="fld">
                    <label>Дата</label>
                    <span>{{ dateLabel }}</span>
                  </div>

                  <div class="fld">
                    <label>Время</label>
                    <span>{{ clientForm.slot }} — 13:30</span>
                  </div>

                  <button
                    class="btn btn--dark btn--wide"
                    :class="{ 'is-pressed': clientSent }"
                    @click="sendRequest"
                  >
                    {{ clientSent ? 'Заявка отправлена' : 'Отправить заявку' }}
                  </button>
                </div>
              </div>
            </div>

            <div class="monitor__neck"></div>
            <div class="monitor__base"></div>
          </div>

          <div class="phone">
            <div class="phone__screen">
              <div class="phone__notch"></div>

              <div class="phone__hero">
                <img src="/portret.jpg" alt="">
                <span class="phone__hero-title">Заявка</span>
              </div>

              <div class="phone__body">
                <div class="fld fld--sm">
                  <label>Имя</label>
                  <input
                    v-model="clientForm.name"
                    class="inline-input inline-input--sm"
                    type="text"
                    maxlength="24"
                  >
                </div>

                <div class="fld fld--sm">
                  <label>Зал</label>
                  <div class="chips">
                    <span
                      v-for="r in rooms"
                      :key="r"
                      class="chip"
                      :class="{ 'chip--active': r === clientForm.room }"
                      @click="clientForm.room = r"
                    >
                      {{ r }}
                    </span>
                  </div>
                </div>

                <div class="fld fld--sm">
                  <label>Дата</label>
                  <div class="dates">
                    <span
                      v-for="d in dateOptions"
                      :key="d.id"
                      class="date"
                      :class="{ 'date--active': d.id === clientForm.date }"
                      @click="clientForm.date = d.id"
                    >
                      <b>{{ d.num }}</b><em>{{ d.day }}</em>
                    </span>
                  </div>
                </div>

                <div class="fld fld--sm">
                  <label>Время</label>
                  <div class="slots">
                    <span
                      v-for="s in slotOptions"
                      :key="s.id"
                      class="slot"
                      :class="{ 'slot--active': s.id === clientForm.slot }"
                      @click="clientForm.slot = s.id"
                    >
                      {{ s.label }}
                    </span>
                  </div>
                </div>

                <button
                  class="btn btn--dark btn--wide btn--sm"
                  :class="{ 'is-pressed': clientSent }"
                  @click="sendRequest"
                >
                  {{ clientSent ? 'Отправлено' : 'Отправить' }}
                </button>
              </div>
            </div>
          </div>
        </div>

        <div class="note">
          <span class="note__dot"></span>
          <span class="note__line"></span>
          <span class="note__text">Заполняет форму и отправляет</span>
        </div>
      </div>

      <!-- ЦЕНТР: поток (скрывается на мобилке) -->
      <div class="flow" aria-hidden="true">
        <span class="flow__line"></span>
        <span class="flow__caption">заявка</span>
        <span class="flow__arrow">→</span>
      </div>

      <!-- ПРАВО: АДМИН -->
      <div
        class="side side--admin"
        :class="{ 'is-hidden-mobile': mobileSide !== 'admin' }"
      >
        <div class="side__head">
          <span class="side__num">02</span>
          <span class="side__name">Админ</span>
        </div>

        <div class="composition">
          <div class="phone">
            <div class="phone__screen">
              <div class="phone__notch"></div>

              <div class="phone__hero">
                <img src="/transport.png" alt="">
                <span class="phone__hero-title">Входящие</span>
              </div>

              <div class="phone__body">
                <div
                  v-for="row in visibleRows.slice(0, 3)"
                  :key="row.id"
                  class="mini"
                  :class="{ 'mini--active': row.id === adminActive }"
                  @click="adminActive = row.id"
                >
                  <span class="mini__avatar">{{ row.initial }}</span>
                  <span class="mini__body">
                    <b>{{ row.name }}</b>
                    <em>{{ row.room }} · {{ row.time }}</em>
                  </span>
                  <span class="status" :class="'status--' + row.status">
                    {{ row.statusLabel }}
                  </span>
                </div>

                <div v-if="!visibleRows.length" class="empty empty--sm">
                  Пока нет заявок
                </div>
              </div>
            </div>
          </div>

          <div class="monitor">
            <div class="monitor__screen">
              <div class="monitor__bar">
                <span></span><span></span><span></span>
                <em>loft-kadr.app / admin</em>
              </div>

              <div class="monitor__content monitor__content--admin">
                <div class="table__head">
                  <span>Входящие заявки</span>
                  <em>Сегодня · {{ allCount }}</em>
                </div>

                <div class="tabs">
                  <button
                    class="tab"
                    :class="{ 'tab--active': adminTab === 'new' }"
                    @click="adminTab = 'new'"
                  >
                    Новые · {{ newCount }}
                  </button>
                  <button
                    class="tab"
                    :class="{ 'tab--active': adminTab === 'all' }"
                    @click="adminTab = 'all'"
                  >
                    Все · {{ allCount }}
                  </button>
                </div>

                <div class="table">
                  <div class="table__row table__row--head">
                    <span>Клиент</span>
                    <span>Зал</span>
                    <span>Дата</span>
                    <span>Время</span>
                    <span>Статус</span>
                  </div>

                  <div
                    v-for="row in visibleRows"
                    :key="row.id"
                    class="table__row"
                    :class="{ 'table__row--active': row.id === adminActive }"
                    @click="adminActive = row.id"
                  >
                    <span class="table__name">{{ row.name }}</span>
                    <span>{{ row.room }}</span>
                    <span>{{ row.date }}</span>
                    <span>{{ row.time }}</span>
                    <span class="status" :class="'status--' + row.status">
                      {{ row.statusLabel }}
                    </span>
                  </div>

                  <div v-if="!visibleRows.length" class="empty">
                    Пока нет заявок в этом фильтре
                  </div>
                </div>

                <div class="table__actions">
                  <button
                    class="btn btn--ghost btn--sm"
                    :class="{ 'is-rejected': activeRow && activeRow.status === 'rej' }"
                    :disabled="!adminActive"
                    @click="toggleReject"
                  >
                    {{ activeRow && activeRow.status === 'rej'
                        ? 'Снять отклонение'
                        : 'Отклонить' }}
                  </button>

                  <button
                    class="btn btn--accent btn--sm"
                    :class="{ 'is-pressed': activeRow && activeRow.status === 'ok' }"
                    :disabled="!adminActive"
                    @click="toggleConfirm"
                  >
                    {{ activeRow && activeRow.status === 'ok'
                        ? 'Снять подтверждение'
                        : 'Подтвердить' }}
                  </button>
                </div>
              </div>
            </div>

            <div class="monitor__neck"></div>
            <div class="monitor__base"></div>
          </div>
        </div>

        <div class="note note--right">
          <span class="note__text">Видит заявку и подтверждает</span>
          <span class="note__line"></span>
          <span class="note__dot"></span>
        </div>
      </div>
    </div>

    <div class="cabinet__sign">
      <span class="cabinet__sign-name">Лофт «Кадр»</span>
      <span class="cabinet__sign-line">Кабинет · 2026</span>
    </div>
  </section>
</template>

<script setup>
import {
  ref,
  reactive,
  computed,
  watchEffect,
  onMounted,
  onBeforeUnmount,
  nextTick,
} from 'vue'

/**
 * 4.vue — четвёртый блок.
 *
 * Мобильная версия:
 *  · тоглер «Клиент / Админ» сверху;
 *  · показывается одна сторона;
 *  · телефон накладывается поверх монитора (правый нижний угол для клиента,
 *    левый нижний — для админа), свисая вниз;
 *  · таблица в админ-мониторе сжимается с 5 до 4 колонок (дата убирается);
 *  · всё умещается в один экран без внешнего скролла.
 */

const root = ref(null)
const visible = ref(false)
let observer = null

/* --- Мобильный тоглер --- */
const mobileSide = ref('client')   // 'client' | 'admin'

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

/* --- Клиент --- */

const rooms = ['B2', 'B1', 'A1']

const dateOptions = [
  { id: '13', num: '13', day: 'Пн' },
  { id: '14', num: '14', day: 'Вт' },
  { id: '17', num: '17', day: 'Пт' },
]

const slotOptions = [
  { id: '12:30', label: '12:30' },
  { id: '13:45', label: '13:45' },
]

const clientForm = reactive({
  name: 'Анна К.',
  room: 'B2',
  date: '13',
  slot: '12:30',
})

const clientSent = ref(false)
let clientSentTimer = null

const dateLabel = computed(() => {
  const d = dateOptions.find((o) => o.id === clientForm.date)
  return d ? `${d.num} ${d.day}` : ''
})

let uid = 100

function sendRequest() {
  uid += 1
  const id = 'n' + uid

  adminRows.unshift({
    id,
    initial: (clientForm.name.charAt(0) || '?').toUpperCase(),
    name: clientForm.name.trim() || 'Без имени',
    room: clientForm.room,
    date: dateLabel.value,
    time: clientForm.slot,
    status: 'new',
    statusLabel: 'Новая',
  })

  adminTab.value = 'new'
  adminActive.value = id

  clientSent.value = true
  if (clientSentTimer) clearTimeout(clientSentTimer)
  clientSentTimer = setTimeout(() => {
    clientSent.value = false
  }, 1800)
}

/* --- Админ --- */

const adminRows = reactive([
  { id: 'r1', initial: 'А', name: 'Анна К.',   room: 'B2', date: '13 Пн', time: '12:30', status: 'new',  statusLabel: 'Новая'        },
  { id: 'r2', initial: 'М', name: 'Максим Д.', room: 'A1', date: '14 Вт', time: '15:00', status: 'ok',   statusLabel: 'Подтверждена' },
  { id: 'r3', initial: 'О', name: 'Ольга В.',  room: 'C1', date: '17 Пт', time: '18:30', status: 'done', statusLabel: 'Готово'       },
  { id: 'r4', initial: 'И', name: 'Игорь С.',  room: 'B1', date: '19 Вс', time: '11:00', status: 'new',  statusLabel: 'Новая'        },
])

const adminTab = ref('new')
const adminActive = ref('r1')

const newRows = computed(() => adminRows.filter((r) => r.status === 'new'))
const visibleRows = computed(() =>
  adminTab.value === 'new' ? newRows.value : adminRows
)
const newCount = computed(() => newRows.value.length)
const allCount = computed(() => adminRows.length)

const activeRow = computed(
  () => adminRows.find((r) => r.id === adminActive.value) || null
)

watchEffect(() => {
  const list = visibleRows.value
  if (!list.length) {
    adminActive.value = null
    return
  }
  if (!list.some((r) => r.id === adminActive.value)) {
    adminActive.value = list[0].id
  }
})

function toggleConfirm() {
  const row = activeRow.value
  if (!row) return

  if (row.status === 'ok') {
    row.status = 'new'
    row.statusLabel = 'Новая'
  } else {
    row.status = 'ok'
    row.statusLabel = 'Подтверждена'
  }
}

function toggleReject() {
  const row = activeRow.value
  if (!row) return

  if (row.status === 'rej') {
    row.status = 'new'
    row.statusLabel = 'Новая'
  } else {
    row.status = 'rej'
    row.statusLabel = 'Отклонена'
  }
}
</script>

<style scoped lang="scss">
@use "../styles/variables" as *;

/* ==========================================================================
   ПЕРЕМЕННЫЕ
   ========================================================================== */

$text:        #f4ecdf;
$muted:       rgba(244, 236, 223, 0.65);
$muted-2:     rgba(244, 236, 223, 0.45);

$paper:       #ede0c8;
$paper-deep:  #d9c7a6;

$ink:         #1a1108;
$ink-soft:    rgba(26, 17, 8, 0.65);

$accent:      #c8874a;
$accent-deep: #8a5a2c;
$accent-soft: #e0b78a;

$espresso:    #100a06;
$espresso-2:  #1a120c;

$padding-x:      4vw;
$padding-top:    4vh;
$padding-bottom: 4vh;

$label-size:      0.8125rem;
$label-spacing:   0.28em;
$label-weight:    600;

$title-size:    2.75rem;
$title-weight:  300;
$title-spacing: -0.02em;

$mono: "IBM Plex Mono", "JetBrains Mono", ui-monospace,
       SFMono-Regular, Menlo, Consolas, monospace;

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

@keyframes device-in {
  from { opacity: 0; transform: translateY(28px) scale(1.03); }
  to   { opacity: 1; transform: translateY(0)    scale(1);    }
}

@keyframes img-in {
  from { transform: scale(1.06); }
  to   { transform: scale(1);    }
}

@keyframes line-grow {
  from { transform: scaleX(0); }
  to   { transform: scaleX(1); }
}

/* ==========================================================================
   БЛОК
   ========================================================================== */

.cabinet {
  position: relative;

  display: flex;
  flex-direction: column;

  width: $size-full;
  height: $size-full;

  padding: $padding-top $padding-x $padding-bottom;

  color: $text;

  overflow: hidden;

  &__backdrop {
    position: absolute;
    inset: $size-zero;

    background-color: rgba(0, 0, 0, 0.32);

    backdrop-filter: blur(32px) saturate(110%);
    -webkit-backdrop-filter: blur(32px) saturate(110%);

    pointer-events: none;
    z-index: $size-zero;

    opacity: 0;
    .cabinet.is-visible & {
      animation: fade-in 1.4s $ease-soft 0.05s both;
    }
  }

  &__head {
    position: relative;
    z-index: 20;

    display: grid;
    grid-template-columns: 1fr auto;
    align-items: end;

    gap: $space-sm;

    flex: $flex-none;
    margin-bottom: 1.5vh;

    > * { opacity: 0; }

    .cabinet.is-visible & > * {
      animation: fade-down 0.9s $ease-soft both;
    }

    .cabinet.is-visible & > *:nth-child(1) { animation-delay: 0.15s; }
    .cabinet.is-visible & > *:nth-child(2) { animation-delay: 0.28s; }
    .cabinet.is-visible & > *:nth-child(3) { animation-delay: 0.40s; }
  }

  &__label,
  &__sign-name,
  &__sign-line {
    font-size: $label-size;
    font-weight: $label-weight;
    letter-spacing: $label-spacing;
    text-transform: uppercase;
  }

  &__label { color: $muted; }

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
    font-size: 0.75rem;
    letter-spacing: 0.18em;
    color: $muted;
  }

  // --- Мобильный тоглер (скрыт по умолчанию, включается в медиа) ---
  &__toggle {
    display: none;
  }

  &__stage {
    position: relative;
    z-index: 1;

    flex: $flex-grow;
    min-height: $size-zero;

    display: grid;
    grid-template-columns: 1fr auto 1fr;
    align-items: center;
    gap: 1.2vw;
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
    .cabinet.is-visible & {
      animation: fade-in 1s $ease-soft 1.6s both;
    }

    &-name { color: $text; }
    &-line { color: $muted; }
  }
}

/* ==========================================================================
   СТОРОНА
   ========================================================================== */

.side {
  position: relative;

  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 16px;

  width: $size-full;
  min-width: $size-zero;

  &__head {
    display: flex;
    align-items: baseline;
    gap: 12px;

    font-family: $mono;
    font-size: 0.875rem;
    letter-spacing: 0.18em;
    text-transform: uppercase;

    opacity: 0;
    .cabinet.is-visible & {
      animation: fade-down 0.9s $ease-soft 0.45s both;
    }
  }

  &__num {
    font-weight: 700;
    color: $accent;
  }

  &__name {
    color: $muted;
  }

  .note {
    display: flex;
    align-items: center;
    gap: 12px;

    font-family: $mono;
    font-size: 0.75rem;
    letter-spacing: 0.16em;
    text-transform: uppercase;
    color: $muted;

    opacity: 0;
    .cabinet.is-visible & {
      animation: fade-in 0.9s $ease-soft 1.3s both;
    }

    &__dot {
      width: 7px;
      height: 7px;
      border-radius: 50%;
      background: $accent;
      flex: none;
    }

    &__line {
      width: 46px;
      height: 1px;
      background: currentColor;
      opacity: 0.55;
      flex: none;

      transform-origin: left center;
      .cabinet.is-visible & {
        animation: line-grow 0.7s $ease-soft 1.35s both;
      }
    }

    &__text { white-space: nowrap; }

    &--right { flex-direction: row-reverse; }
  }
}

/* ==========================================================================
   КОМПОЗИЦИЯ
   ========================================================================== */

.composition {
  position: relative;

  display: flex;
  align-items: flex-end;
  justify-content: center;
  gap: 24px;

  width: $size-full;

  transform: translateY(-48px);

  .side--client & { flex-direction: row; }
  .side--admin  & { flex-direction: row-reverse; }
}

/* ==========================================================================
   МОНИТОР
   ========================================================================== */

.monitor {
  display: flex;
  flex-direction: column;
  align-items: center;

  flex: 1 1 auto;
  min-width: $size-zero;
  max-width: 620px;

  opacity: 0;
  .cabinet.is-visible .side--client & {
    animation: device-in 1.1s $ease-soft 0.55s both;
  }
  .cabinet.is-visible .side--admin & {
    animation: device-in 1.1s $ease-soft 0.70s both;
  }

  &__screen {
    width: $size-full;
    aspect-ratio: 16 / 10;

    background-color: $espresso-2;
    border: 12px solid #060403;
    border-radius: 16px;

    box-shadow:
      0 40px 80px rgba(0, 0, 0, 0.7),
      0 0 0 1px rgba(255, 255, 255, 0.04) inset;

    overflow: hidden;

    display: flex;
    flex-direction: column;
  }

  &__bar {
    flex: none;

    display: flex;
    align-items: center;
    gap: 8px;

    height: 32px;
    padding: 0 14px;

    background: rgba(0, 0, 0, 0.4);
    border-bottom: 1px solid rgba(255, 255, 255, 0.05);

    span {
      width: 10px;
      height: 10px;
      border-radius: 50%;

      &:nth-child(1) { background: rgba(220, 120, 90, 0.65); }
      &:nth-child(2) { background: rgba(220, 180, 90, 0.65); }
      &:nth-child(3) { background: rgba(140, 180, 110, 0.65); }
    }

    em {
      margin-left: 12px;

      font-family: $mono;
      font-size: 0.75rem;
      letter-spacing: 0.06em;
      color: $muted-2;
      font-style: normal;
    }
  }

  // --- рабочий скролл внутри монитора ---
  &__content {
    flex: $flex-fill;
    min-height: $size-zero;

    display: flex;
    flex-direction: column;
    gap: 14px;

    padding: 22px;

    background-color: $espresso-2;
    color: $text;

    overflow-y: auto;
    overflow-x: hidden;
    overscroll-behavior: contain;
    -webkit-overflow-scrolling: touch;

    scrollbar-width: thin;
    scrollbar-color: rgba(200, 135, 74, 0.5) transparent;

    &::-webkit-scrollbar { width: 6px; }
    &::-webkit-scrollbar-track { background: transparent; }
    &::-webkit-scrollbar-thumb {
      background: rgba(200, 135, 74, 0.45);
      border-radius: 3px;

      &:hover { background: rgba(200, 135, 74, 0.7); }
    }
  }

  &__neck {
    width: 100px;
    height: 22px;

    background: linear-gradient(to bottom, #060403, #030201);
    border-radius: 0 0 5px 5px;
  }

  &__base {
    width: 200px;
    height: 9px;

    background: #060403;
    border-radius: 5px;

    box-shadow: 0 12px 26px rgba(0, 0, 0, 0.55);
  }
}

/* ==========================================================================
   МОНИТОР: КЛИЕНТ
   ========================================================================== */

.monitor__content--client {
  flex-direction: row !important;
  gap: 20px !important;

  .fld label { color: $muted-2; }
  .fld span  { color: $paper; }
}

.dash__hero {
  flex: 0 0 44%;

  position: relative;

  border-radius: 14px;
  overflow: hidden;

  img {
    width: $size-full;
    height: $size-full;
    object-fit: cover;

    filter: sepia(0.15) saturate(0.9) brightness(0.7);
  }
}

.dash__hero-copy {
  position: absolute;
  left: 18px;
  right: 18px;
  bottom: 18px;

  display: flex;
  flex-direction: column;
  gap: 3px;
}

.dash__kicker {
  font-family: $mono;
  font-size: 0.75rem;
  letter-spacing: 0.22em;
  text-transform: uppercase;
  color: $accent-soft;
}

.dash__title {
  font-family: Georgia, "Times New Roman", serif;
  font-size: 1.75rem;
  font-weight: 700;
  color: $paper;
}

.dash__form {
  flex: $flex-fill;
  min-width: $size-zero;

  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-auto-rows: min-content;
  gap: 16px 22px;

  align-content: start;

  .btn--wide {
    grid-column: 1 / -1;
    margin-top: 8px;
  }
}

/* ==========================================================================
   МОНИТОР: АДМИН
   ========================================================================== */

.monitor__content--admin {
  gap: 12px !important;

  > * { flex-shrink: 0; }

  .table {
    flex: 0 0 auto;
    overflow: visible;
  }
}

.table__head {
  display: flex;
  align-items: baseline;
  justify-content: space-between;

  padding-bottom: 8px;

  border-bottom: 1px solid rgba(255, 255, 255, 0.06);

  span {
    font-size: 1.125rem;
    font-weight: 600;
    color: $paper;
  }

  em {
    font-family: $mono;
    font-size: 0.75rem;
    letter-spacing: 0.16em;
    text-transform: uppercase;
    color: $muted-2;
    font-style: normal;
  }
}

/* ==========================================================================
   ТАБЫ
   ========================================================================== */

.tabs {
  display: flex;
  gap: 6px;

  padding: 3px;

  background-color: rgba(255, 255, 255, 0.04);
  border-radius: 999px;
}

.tab {
  flex: 1;

  padding: 6px 10px;

  font-family: $mono;
  font-size: 0.6875rem;
  letter-spacing: 0.14em;
  text-transform: uppercase;

  background: transparent;
  border: 0;
  border-radius: 999px;

  color: $muted;

  cursor: pointer;
  transition: color 0.2s ease, background-color 0.25s ease;

  &--active {
    background-color: rgba(200, 135, 74, 0.18);
    color: $paper;
  }

  &:hover:not(&--active) { color: $paper; }
}

/* ==========================================================================
   ТАБЛИЦА
   ========================================================================== */

.table {
  display: flex;
  flex-direction: column;
  gap: 4px;

  flex: 1 1 auto;
  min-height: $size-zero;
}

.table__row {
  display: grid;
  grid-template-columns: 1.4fr 0.6fr 0.9fr 0.8fr 1.1fr;
  align-items: center;
  gap: 10px;

  padding: 10px 12px;

  font-size: 0.9375rem;
  color: $muted;

  border-radius: 10px;
  cursor: pointer;

  transition:
    background-color 0.2s ease,
    color            0.2s ease;

  &--head {
    padding: 4px 12px;

    font-family: $mono;
    font-size: 0.6875rem;
    letter-spacing: 0.16em;
    text-transform: uppercase;
    color: $muted-2;

    cursor: default;
    border-bottom: 1px dashed rgba(255, 255, 255, 0.05);
    border-radius: 0;
  }

  &--active {
    background-color: rgba(200, 135, 74, 0.16);
    color: $text;
  }

  &:hover:not(&--head) {
    background-color: rgba(200, 135, 74, 0.08);
  }
}

.table__name {
  font-weight: 600;
  color: $paper;
}

.table__actions {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 12px;

  margin-top: auto;
}

.empty {
  display: grid;
  place-items: center;

  padding: 22px 12px;

  font-family: $mono;
  font-size: 0.75rem;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: $muted-2;

  border: 1px dashed rgba(255, 255, 255, 0.08);
  border-radius: 10px;

  &--sm {
    padding: 14px 8px;
    font-size: 0.625rem;
  }
}

/* ==========================================================================
   ТЕЛЕФОН
   ========================================================================== */

.phone {
  flex: 0 0 auto;
  width: 230px;

  opacity: 0;
  .cabinet.is-visible .side--client & {
    animation: device-in 1.1s $ease-soft 0.75s both;
  }
  .cabinet.is-visible .side--admin & {
    animation: device-in 1.1s $ease-soft 0.90s both;
  }

  &__screen {
    position: relative;

    width: $size-full;
    aspect-ratio: 9 / 19.5;

    background-color: $espresso;
    border: 8px solid #060403;
    border-radius: 34px;

    box-shadow:
      0 36px 72px rgba(0, 0, 0, 0.7),
      0 0 0 1px rgba(255, 255, 255, 0.06) inset;

    overflow: hidden;
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

    z-index: 3;
  }

  &__hero {
    position: relative;

    height: 26%;
    overflow: hidden;

    img {
      position: absolute;
      inset: $size-zero;

      width: $size-full;
      height: $size-full;
      object-fit: cover;

      filter: sepia(0.2) saturate(0.85) brightness(0.6);

      transform: scale(1.06);
      .cabinet.is-visible & {
        animation: img-in 2s $ease-soft 0.9s both;
      }
    }

    &::after {
      content: "";
      position: absolute;
      inset: $size-zero;

      background: linear-gradient(
        to bottom,
        rgba(16, 10, 6, 0.3) 0%,
        rgba(16, 10, 6, 0.0)  40%,
        rgba(16, 10, 6, 0.85) 100%
      );
    }
  }

  &__hero-title {
    position: absolute;
    left: 12px;
    right: 12px;
    bottom: 10px;

    font-family: Georgia, "Times New Roman", serif;
    font-size: 1.0625rem;
    font-weight: 700;
    color: $paper;
    text-shadow: 0 2px 10px rgba(0, 0, 0, 0.7);

    z-index: 2;
  }

  &__body {
    height: 74%;

    display: flex;
    flex-direction: column;
    gap: 10px;

    padding: 14px;

    background-color: $paper;
    color: $ink;

    overflow-y: auto;
    overscroll-behavior: contain;
    scrollbar-width: none;
    &::-webkit-scrollbar { display: none; }

    .status {
      font-weight: 700;

      &--new {
        background-color: rgba(200, 135, 74, 0.95);
        color: #ffffff;
      }

      &--ok {
        background-color: rgba(102, 138, 70, 0.95);
        color: #ffffff;
      }

      &--rej {
        background-color: rgba(170, 62, 48, 0.95);
        color: #ffffff;
      }

      &--done {
        background-color: rgba(26, 17, 8, 0.85);
        color: #ffffff;
      }
    }
  }
}

/* ==========================================================================
   ПОЛЯ ФОРМЫ
   ========================================================================== */

.fld {
  display: flex;
  flex-direction: column;
  gap: 4px;

  label {
    font-family: $mono;
    font-size: 0.6875rem;
    letter-spacing: 0.16em;
    text-transform: uppercase;
    color: $ink-soft;
  }

  span {
    font-size: 1.0625rem;
    font-weight: 600;
    color: $ink;
  }

  &--sm {
    label { font-size: 0.5625rem; }
    span  { font-size: 0.875rem; }
  }
}

.inline-input {
  width: 100%;
  padding: 2px 0;

  font-family: inherit;
  font-size: 1.0625rem;
  font-weight: 600;
  color: $paper;

  background: transparent;
  border: 0;
  border-bottom: 1px solid rgba(244, 236, 223, 0.2);
  outline: none;

  transition: border-color 0.2s ease;

  &:focus { border-bottom-color: $accent; }

  &--sm {
    font-size: 0.875rem;
    color: $ink;
    border-bottom-color: rgba(26, 17, 8, 0.2);

    &:focus { border-bottom-color: $accent; }
  }
}

/* ==========================================================================
   ЧИПСЫ / ДАТЫ / СЛОТЫ
   ========================================================================== */

.chips {
  display: flex;
  gap: 5px;
}

.chip {
  padding: 4px 10px;

  font-size: 0.6875rem;
  font-weight: 500;

  background-color: rgba(26, 17, 8, 0.08);
  color: $ink-soft;
  border-radius: 999px;

  cursor: pointer;
  transition: background-color 0.2s ease, color 0.2s ease;

  &--active {
    background-color: $accent;
    color: $paper;
  }
}

.dates {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 5px;
}

.date {
  display: flex;
  align-items: baseline;
  justify-content: center;
  gap: 5px;

  padding: 7px 0;

  background-color: rgba(26, 17, 8, 0.06);
  border: 1px solid transparent;
  border-radius: 10px;

  cursor: pointer;
  transition: background-color 0.2s ease, border-color 0.2s ease;

  b {
    font-size: 0.9375rem;
    font-weight: 600;
    color: $ink;
  }

  em {
    font-size: 0.5625rem;
    font-style: normal;
    color: $ink-soft;
  }

  &--active {
    background-color: #fff;
    border-color: $ink;
  }
}

.slots {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 5px;
}

.slot {
  padding: 8px 4px;

  font-size: 0.6875rem;
  font-weight: 500;
  text-align: center;

  background-color: rgba(26, 17, 8, 0.06);
  border: 1px solid transparent;
  border-radius: 10px;

  cursor: pointer;
  transition: background-color 0.2s ease, border-color 0.2s ease;

  &--active {
    background-color: #fff;
    border-color: $ink;
    color: $ink;
  }
}

/* ==========================================================================
   МИНИ-СПИСОК
   ========================================================================== */

.mini {
  display: grid;
  grid-template-columns: 28px 1fr auto;
  align-items: center;
  gap: 8px;

  padding: 8px;

  background-color: rgba(26, 17, 8, 0.05);
  border: 1px solid transparent;
  border-radius: 12px;

  cursor: pointer;
  transition:
    background-color 0.2s ease,
    border-color     0.2s ease;

  &--active {
    background-color: rgba(200, 135, 74, 0.16);
    border-color: rgba(138, 90, 44, 0.45);
  }

  &__avatar {
    display: grid;
    place-items: center;

    width: 28px;
    height: 28px;

    font-family: $mono;
    font-size: 0.6875rem;
    font-weight: 700;

    background-color: $accent-deep;
    color: $paper;
    border-radius: 50%;
  }

  &__body {
    display: flex;
    flex-direction: column;
    gap: 1px;

    min-width: 0;

    b {
      font-size: 0.875rem;
      font-weight: 600;
      color: $ink;

      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }

    em {
      font-family: $mono;
      font-size: 0.5625rem;
      font-style: normal;
      letter-spacing: 0.04em;
      color: $ink-soft;
    }
  }
}

/* ==========================================================================
   СТАТУСЫ
   ========================================================================== */

.status {
  font-family: $mono;
  font-size: 0.625rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;

  padding: 3px 8px;
  border-radius: 999px;

  white-space: nowrap;

  &--new {
    background-color: rgba(200, 135, 74, 0.24);
    color: $accent-soft;
  }

  &--ok {
    background-color: rgba(180, 205, 130, 0.2);
    color: #d5e2a4;
  }

  &--rej {
    background-color: rgba(200, 100, 80, 0.22);
    color: #e0a89a;
  }

  &--done {
    background-color: rgba(244, 236, 223, 0.08);
    color: $muted;
  }
}

/* ==========================================================================
   КНОПКИ
   ========================================================================== */

.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;

  padding: 12px 18px;

  font-size: 0.8125rem;
  font-weight: 600;
  letter-spacing: 0.02em;

  border: 1px solid transparent;
  border-radius: 999px;

  cursor: pointer;
  transition:
    filter           0.2s ease,
    background-color 0.3s $ease-soft,
    color            0.3s $ease-soft,
    border-color     0.3s $ease-soft;

  &:hover:not(:disabled) { filter: brightness(1.06); }
  &:active:not(:disabled) { transform: translateY(1px); }

  &:disabled {
    opacity: 0.4;
    cursor: not-allowed;
  }

  &--dark {
    background-color: $ink;
    color: $paper;

    &.is-pressed {
      background-color: $accent-deep;
      color: $paper;
    }
  }

  &--accent {
    background-color: $accent;
    color: $paper;

    &.is-pressed { background-color: $accent-deep; }
  }

  &--ghost {
    background-color: transparent;
    color: $muted;
    border-color: rgba(244, 236, 223, 0.18);

    &:hover:not(:disabled) {
      color: $paper;
      border-color: rgba(244, 236, 223, 0.35);
    }

    &.is-rejected {
      background-color: rgba(170, 62, 48, 0.22);
      color: #e0a89a;
      border-color: rgba(170, 62, 48, 0.55);
    }
  }

  &--wide { width: $size-full; }
  &--sm   { padding: 8px 12px; font-size: 0.75rem; }
}

/* ==========================================================================
   ПОТОК
   ========================================================================== */

.flow {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 10px;

  min-width: 3vw;

  opacity: 0;
  .cabinet.is-visible & {
    animation: fade-in 0.9s $ease-soft 1.0s both;
  }

  &__line {
    width: 100%;
    height: 1px;

    background: linear-gradient(
      to right,
      rgba(200, 135, 74, 0.1),
      rgba(200, 135, 74, 0.9),
      rgba(200, 135, 74, 0.1)
    );

    transform-origin: center;
    .cabinet.is-visible & {
      animation: line-grow 1s $ease-soft 1.05s both;
    }
  }

  &__arrow {
    font-family: $mono;
    font-size: 1.75rem;
    line-height: 1;
    color: $accent;
  }

  &__caption {
    font-family: $mono;
    font-size: 0.75rem;
    letter-spacing: 0.3em;
    text-transform: uppercase;
    color: $muted;
  }
}

/* ==========================================================================
   МОБИЛЬНАЯ ВЕРСИЯ — тоглер «Клиент / Админ», телефон поверх монитора
   ========================================================================== */

@media (max-width: 900px) {

  .cabinet {
    padding: 2.5vh 4vw;
  }

  /* --- Тоглер --- */
  .cabinet__toggle {
    position: relative;
    z-index: 20;

    display: flex;
    gap: 6px;

    margin: 0 0 12px;

    padding: 4px;

    background-color: rgba(255, 255, 255, 0.04);
    border: 1px solid rgba(200, 170, 135, 0.12);
    border-radius: 999px;

    opacity: 0;
    .cabinet.is-visible & {
      animation: fade-down 0.7s $ease-soft 0.4s both;
    }
  }

  .cabinet__toggle-btn {
    flex: 1;

    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;

    padding: 8px 12px;

    font-family: $mono;
    font-size: 0.6875rem;
    letter-spacing: 0.14em;
    text-transform: uppercase;

    color: $muted;

    background: transparent;
    border: 0;
    border-radius: 999px;

    cursor: pointer;
    transition:
      background-color 0.25s $ease-soft,
      color            0.25s $ease-soft;

    &.is-active {
      background-color: rgba(200, 135, 74, 0.22);
      color: $paper;
    }
  }

  .cabinet__toggle-num {
    font-weight: 700;
    color: $accent;
  }

  /* --- Сцена: одна колонка, без среднего flow --- */
  .cabinet__stage {
    display: block;

    > * { min-width: 0; }
  }

  .flow { display: none; }
  .side.is-hidden-mobile { display: none; }

  .side {
    width: 100%;
    align-items: stretch;
    gap: 8px;
  }

  .side__head {
    justify-content: center;
    font-size: 0.75rem;
  }

  /* --- Композиция: монитор во всю ширину, телефон поверх --- */
  .composition {
    position: relative;

    display: block;

    width: 100%;

    transform: none;

    padding-bottom: 42px; /* запас под свисающий телефон */
  }

  .monitor {
    width: 100%;
    max-width: 100%;
  }

  .monitor__screen {
    border-width: 6px;
    border-radius: 10px;
    aspect-ratio: 16 / 11;
  }

  .monitor__bar {
    height: 22px;
    padding: 0 8px;

    em { font-size: 0.5625rem; margin-left: 6px; }

    span { width: 6px; height: 6px; }
  }

  .monitor__content {
    padding: 12px;
    gap: 10px;
  }

  .monitor__neck { width: 60px; height: 12px; }
  .monitor__base { width: 110px; height: 6px; }

  /* --- Клиентский монитор: колонка --- */
  .monitor__content--client {
    flex-direction: column !important;
    gap: 10px !important;
  }

  .dash__hero {
    flex: 0 0 auto;
    aspect-ratio: 16 / 7;
    border-radius: 10px;
  }

  .dash__hero-copy { left: 12px; right: 12px; bottom: 10px; }
  .dash__kicker { font-size: 0.625rem; }
  .dash__title { font-size: 1.25rem; }

  .dash__form {
    grid-template-columns: 1fr 1fr;
    gap: 8px 12px;

    .btn--wide {
      grid-column: 1 / -1;
      margin-top: 4px;
      padding: 9px 12px;
      font-size: 0.75rem;
    }
  }

  .fld {
    gap: 2px;

    label { font-size: 0.5rem; letter-spacing: 0.12em; }
    span  { font-size: 0.8125rem; }
  }

  .inline-input {
    font-size: 0.8125rem;
    padding: 1px 0;
  }

  /* --- Админский монитор: компактная таблица (4 колонки) --- */
  .monitor__content--admin {
    gap: 8px !important;
  }

  .table__head {
    padding-bottom: 6px;

    span { font-size: 0.9375rem; }
    em { font-size: 0.5625rem; }
  }

  .tabs {
    padding: 2px;
  }

  .tab {
    padding: 5px 8px;
    font-size: 0.5625rem;
    letter-spacing: 0.1em;
  }

  /* Прячем колонку «Дата» — 5 → 4 колонки */
  .table__row {
    grid-template-columns: 1.5fr 0.7fr 0.8fr 1fr;
    gap: 4px;

    padding: 6px 8px;

    font-size: 0.6875rem;

    > span:nth-child(3) { display: none; }
  }

  .table__row--head {
    font-size: 0.5rem;
    letter-spacing: 0.1em;
    padding: 3px 8px;
  }

  .table__name { font-size: 0.75rem; }

  .status {
    font-size: 0.5rem;
    padding: 2px 5px;
    letter-spacing: 0.06em;
  }

  .table__actions {
    gap: 6px;
  }

  .btn--sm {
    padding: 7px 10px;
    font-size: 0.6875rem;
  }

  /* --- Телефон: поверх монитора, свисает вниз --- */
  .phone {
    position: absolute;
    bottom: 0;

    width: 100px;

    z-index: 10;

    /* Убираем анимацию сдвига с transform — phone теперь позиционируется абсолютно */
    .cabinet.is-visible & {
      animation: fade-in 0.9s $ease-soft 0.8s both;
    }
  }

  .side--client .phone {
    right: 10px;
    left: auto;
  }

  .side--admin .phone {
    left: 10px;
    right: auto;
  }

  .phone__screen {
    border-width: 5px;
    border-radius: 18px;
  }

  .phone__notch {
    width: 38px;
    height: 11px;
    top: 5px;
  }

  .phone__hero {
    height: 24%;
  }

  .phone__hero-title {
    left: 8px;
    right: 8px;
    bottom: 6px;
    font-size: 0.6875rem;
  }

  .phone__body {
    padding: 8px;
    gap: 6px;
  }

  .fld--sm {
    label { font-size: 0.4375rem; letter-spacing: 0.1em; }
    span  { font-size: 0.6875rem; }
  }

  .inline-input--sm { font-size: 0.6875rem; }

  .chips { gap: 3px; }
  .chip { padding: 3px 6px; font-size: 0.5rem; }

  .dates { gap: 3px; }
  .date {
    padding: 5px 0;
    border-radius: 7px;
    b { font-size: 0.75rem; }
    em { font-size: 0.4375rem; }
  }

  .slots { gap: 3px; }
  .slot {
    padding: 5px 2px;
    font-size: 0.5rem;
    border-radius: 7px;
  }

  .phone .btn {
    padding: 7px 10px;
    font-size: 0.5625rem;
  }

  .mini {
    padding: 6px;
    gap: 6px;
    grid-template-columns: 22px 1fr auto;
    border-radius: 8px;
  }

  .mini__avatar {
    width: 22px;
    height: 22px;
    font-size: 0.5625rem;
  }

  .mini__body {
    b { font-size: 0.6875rem; }
    em { font-size: 0.5rem; }
  }

  .phone .status {
    font-size: 0.4375rem;
    padding: 2px 5px;
  }

  /* --- Ноты под композицией --- */
  .side .note {
    justify-content: center;
    text-align: center;

    font-size: 0.5625rem;

    &__text { white-space: normal; }
    &__line { width: 30px; }
  }

  /* --- Подпись в углу --- */
  .cabinet__sign {
    font-size: 0.5625rem;
  }
}

/* --- Сверх-узкие экраны --- */
@media (max-width: 480px) {

  .cabinet__title { font-size: 2rem; }

  .monitor__screen { aspect-ratio: 16 / 12; }

  .monitor__content { padding: 10px; }

  .dash__title { font-size: 1.125rem; }
  .dash__hero { aspect-ratio: 16 / 8; }

  .table__row {
    grid-template-columns: 1.4fr 0.6fr 0.8fr 1fr;
    font-size: 0.625rem;
    padding: 5px 6px;
  }

  .table__row--head {
    font-size: 0.4375rem;
  }

  .status {
    font-size: 0.4375rem;
    padding: 1px 4px;
  }

  .phone {
    width: 88px;
  }

  .phone__screen {
    border-width: 4px;
    border-radius: 16px;
  }
}
</style>