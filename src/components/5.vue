<!-- 5.vue -->
<template>
  <section ref="root" class="crm" :class="{ 'is-visible': visible }">
    <div class="crm__stage">
      <!-- ЛЕВАЯ КОЛОНКА: Метка раздела + Круговой график -->
      <div class="stage__left">
        <span class="section-label">05 — Аналитика</span>
        
        <article class="chart chart--donut">
          <header class="chart__head">
            <span class="chart__title">Клиенты по типу</span>
            <span class="chart__sub">Q1 · всего {{ totalClients }}</span>
          </header>
          <div class="chart__body">
            <div ref="donutEl" class="chart__canvas"></div>
            <ul class="legend">
              <li v-for="s in donutData" :key="s.name" class="legend__row">
                <span class="legend__dot" :style="{ backgroundColor: s.color }"></span>
                <span class="legend__name">{{ s.name }}</span>
                <span class="legend__val">{{ s.value }}</span>
              </li>
            </ul>
          </div>
        </article>
      </div>

      <!-- ПРАВАЯ КОЛОНКА: Всё остальное -->
      <div class="stage__right">
        <!-- KPI -->
        <div class="kpi">
          <article v-for="(k, i) in kpis" :key="k.id" class="kpi__card" :style="{ '--i': i }">
            <span class="kpi__label">{{ k.label }}</span>
            <span class="kpi__value">{{ k.value }}</span>
            <span class="kpi__delta" :class="'kpi__delta--' + k.dir">
              {{ k.dir === 'up' ? '▲' : '▼' }} {{ k.delta }}
            </span>
          </article>
        </div>

        <!-- Средний ряд: Выручка и Динамика -->
        <div class="charts-row">
          <article class="chart chart--bar">
            <header class="chart__head">
              <span class="chart__title">Выручка · 6 мес</span>
              <span class="chart__sub">тыс. ₽ / месяц</span>
            </header>
            <div class="chart__body">
              <div ref="barEl" class="chart__canvas"></div>
            </div>
          </article>

          <article class="chart chart--line">
            <header class="chart__head">
              <span class="chart__title">Динамика клиентов</span>
              <span class="chart__sub">новые и постоянные · 12 недель</span>
            </header>
            <div class="chart__body">
              <div ref="lineEl" class="chart__canvas"></div>
            </div>
          </article>
        </div>

        <!-- Нижний ряд: Залы и Боты -->
        <div class="bottom-row">
          <article class="chart chart--hall">
            <header class="chart__head">
              <span class="chart__title">Загрузка залов</span>
              <span class="chart__sub">% времени</span>
            </header>
            <div class="chart__body">
              <div ref="hallEl" class="chart__canvas"></div>
            </div>
          </article>

          <div class="bots">
            <header class="bots__head">
              <span class="bots__label">Автоматизация · боты</span>
            </header>
            <div class="bots__grid">
              <article class="bot bot--tg">
                <div class="bot__icon" aria-hidden="true">
                  <svg viewBox="0 0 24 24" width="24" height="24">
                    <path fill="currentColor" d="M21.8 4.3 2.9 11.6c-.9.3-.9 1.5.1 1.8l4.5 1.4 1.7 5.2c.2.7 1.2.8 1.6.2l2.4-2.6 4.6 3.4c.6.4 1.4.1 1.6-.6l2.7-15.3c.2-.9-.8-1.6-1.6-1.2zM9.1 14.6l9.4-6.4-7.6 7.5-.2 3.5-1.6-4.6z" />
                  </svg>
                </div>
                <div class="bot__body">
                  <span class="bot__name">Telegram</span>
                  <ul class="bot__metrics">
                    <li><span>Диалогов</span><b>340</b></li>
                    <li><span>Заявок</span><b>182</b></li>
                    <li><span>Конверсия</span><b>53%</b></li>
                  </ul>
                </div>
              </article>

              <article class="bot bot--vk">
                <div class="bot__icon" aria-hidden="true">
                  <svg viewBox="0 0 24 24" width="24" height="24">
                    <path fill="currentColor" d="M12.8 16.4h1.3c.4 0 .5-.3.5-.6 0-.9.6-1.1 1.3-.4 1.2 1.1 2.3 1.1 2.9 1.1h1.6c.5 0 .7-.3.5-.8-.2-.5-.9-1.4-1.8-2.4-.7-.8-.7-1.2 0-2 .5-.6 1.5-1.7 1.8-2.3.3-.5.1-.8-.5-.8h-1.6c-.5 0-.7.3-.9.7-.2.6-.7 1.7-1.4 2.5-.6.7-1 .8-1.2.8-.2 0-.4-.2-.4-.8V9.1c0-.6-.1-.8-.5-.8h-2.6c-.3 0-.5.2-.5.5 0 .5.7.6.8 1.6v2.4c0 .7-.1.8-.3.8-.4 0-1-.5-1.6-1.4-.8-1.1-1.3-2.4-1.5-3-.2-.4-.4-.6-.9-.6H5.3c-.5 0-.7.2-.6.7.2 1 .8 2.5 2 4.1 1.4 1.9 3.2 2.9 5 2.9z M13 11.5v-.1z" />
                  </svg>
                </div>
                <div class="bot__body">
                  <span class="bot__name">VK</span>
                  <ul class="bot__metrics">
                    <li><span>Диалогов</span><b>210</b></li>
                    <li><span>Заявок</span><b>96</b></li>
                    <li><span>Конверсия</span><b>46%</b></li>
                  </ul>
                </div>
              </article>

              <article class="bot bot--total">
                <div class="bot__icon" aria-hidden="true">
                  <span class="bot__icon-glyph">Σ</span>
                </div>
                <div class="bot__body">
                  <span class="bot__name">Итого</span>
                  <ul class="bot__metrics">
                    <li><span>Диалогов</span><b>550</b></li>
                    <li><span>Заявок</span><b>278</b></li>
                    <li><span>Конверсия</span><b>51%</b></li>
                  </ul>
                </div>
              </article>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount, nextTick, watch } from 'vue'
import * as echarts from 'echarts'

const root = ref(null)
const visible = ref(false)
let observer = null
let resizeObs = null

const totalClients = 260
const donutData = [
  { name: 'Постоянные', value: 128, color: '#c8874a' },
  { name: 'Новые',      value:  74, color: '#8a5a2c' },
  { name: 'Подписка',   value:  36, color: '#e0b78a' },
  { name: 'Разовые',    value:  22, color: '#6b4423' },
]

const kpis = [
  { id: 'rev', label: 'Выручка · Q1', value: '1 284 500 ₽', delta: '+18%', dir: 'up' },
  { id: 'cli', label: 'Клиентов',      value: '260',         delta: '+24',  dir: 'up' },
  { id: 'reg', label: 'Постоянных',    value: '128',         delta: '49%',  dir: 'up' },
  { id: 'avg', label: 'Средний чек',   value: '4 940 ₽',     delta: '+6%',  dir: 'up' },
]

const donutEl = ref(null)
const barEl   = ref(null)
const lineEl  = ref(null)
const hallEl  = ref(null)

let donutChart = null
let barChart   = null
let lineChart  = null
let hallChart  = null

const COFFEE_PALETTE = ['#c8874a', '#8a5a2c', '#e0b78a', '#6b4423', '#d9c7a6']

const BASE_TEXT = {
  color: 'rgba(244, 236, 223, 0.95)',
  fontFamily: '"IBM Plex Mono", ui-monospace, SFMono-Regular, Menlo, monospace',
  fontSize: 14,
}

const AXIS_LINE = { lineStyle: { color: 'rgba(244, 236, 223, 0.2)' } }
const SPLIT_LINE = { lineStyle: { color: 'rgba(244, 236, 223, 0.1)' } }

const TOOLTIP = {
  backgroundColor: 'rgba(0, 0, 0, 0.9)',
  borderColor: 'rgba(200, 135, 74, 0.4)',
  borderWidth: 1,
  textStyle: { color: '#f4ecdf', fontSize: 14 },
  extraCssText: 'border-radius: 8px; padding: 10px 14px;',
}

function initCharts() {
  if (donutEl.value && !donutChart) {
    donutChart = echarts.init(donutEl.value, null, { renderer: 'canvas' })
    donutChart.setOption({
      color: COFFEE_PALETTE,
      textStyle: BASE_TEXT,
      tooltip: { ...TOOLTIP, trigger: 'item', formatter: '{b}: {c} ({d}%)' },
      series: [{
        type: 'pie',
        radius: ['58%', '78%'],
        center: ['50%', '50%'],
        avoidLabelOverlap: true,
        itemStyle: { borderColor: 'rgba(0,0,0,0.5)', borderWidth: 2, borderRadius: 6 },
        label: { show: false },
        labelLine: { show: false },
        emphasis: {
          scale: true,
          scaleSize: 8,
          itemStyle: { shadowBlur: 20, shadowColor: 'rgba(200, 135, 74, 0.5)' },
        },
        data: donutData.map((d) => ({ value: d.value, name: d.name, itemStyle: { color: d.color } })),
      }],
    })
  }

  if (barEl.value && !barChart) {
    barChart = echarts.init(barEl.value, null, { renderer: 'canvas' })
    const months = ['Окт', 'Ноя', 'Дек', 'Янв', 'Фев', 'Мар']
    const rev = [148, 172, 210, 236, 268, 320]
    barChart.setOption({
      textStyle: BASE_TEXT,
      grid: { top: 10, right: 10, bottom: 30, left: 40 },
      tooltip: { ...TOOLTIP, trigger: 'axis', axisPointer: { type: 'shadow' } },
      xAxis: {
        type: 'category', data: months, axisLine: AXIS_LINE, axisTick: { show: false },
        axisLabel: { color: 'rgba(244, 236, 223, 0.8)', fontSize: 13 },
      },
      yAxis: {
        type: 'value', axisLine: { show: false }, axisTick: { show: false }, splitLine: SPLIT_LINE,
        axisLabel: { color: 'rgba(244, 236, 223, 0.7)', fontSize: 13 },
      },
      series: [{
        type: 'bar', data: rev, barWidth: '50%',
        itemStyle: {
          color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
            { offset: 0, color: '#c8874a' }, { offset: 1, color: '#8a5a2c' },
          ]),
          borderRadius: [6, 6, 0, 0],
        },
        emphasis: { itemStyle: { shadowBlur: 22, shadowColor: 'rgba(200, 135, 74, 0.5)' } },
      }],
    })
  }

  if (lineEl.value && !lineChart) {
    lineChart = echarts.init(lineEl.value, null, { renderer: 'canvas' })
    const weeks = ['W1', 'W2', 'W3', 'W4', 'W5', 'W6', 'W7', 'W8', 'W9', 'W10', 'W11', 'W12']
    const fresh = [12, 18, 16, 22, 20, 28, 26, 32, 30, 36, 34, 40]
    const regular = [28, 32, 34, 38, 40, 42, 46, 48, 52, 54, 58, 62]
    lineChart.setOption({
      textStyle: BASE_TEXT,
      grid: { top: 30, right: 15, bottom: 30, left: 40 },
      tooltip: { ...TOOLTIP, trigger: 'axis', axisPointer: { type: 'line', lineStyle: { color: 'rgba(200, 135, 74, 0.4)' } } },
      legend: {
        top: 0, right: 0, icon: 'circle', itemWidth: 10, itemHeight: 10,
        textStyle: { color: 'rgba(244, 236, 223, 0.9)', fontSize: 13 },
      },
      xAxis: {
        type: 'category', boundaryGap: false, data: weeks, axisLine: AXIS_LINE, axisTick: { show: false },
        axisLabel: { color: 'rgba(244, 236, 223, 0.8)', fontSize: 13 },
      },
      yAxis: {
        type: 'value', axisLine: { show: false }, axisTick: { show: false }, splitLine: SPLIT_LINE,
        axisLabel: { color: 'rgba(244, 236, 223, 0.7)', fontSize: 13 },
      },
      series: [
        {
          name: 'Новые', type: 'line', smooth: true, symbol: 'circle', symbolSize: 8, data: fresh,
          lineStyle: { width: 3, color: '#c8874a' },
          itemStyle: { color: '#c8874a', borderColor: 'rgba(0,0,0,0.5)', borderWidth: 2 },
          areaStyle: {
            color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
              { offset: 0, color: 'rgba(200, 135, 74, 0.4)' }, { offset: 1, color: 'rgba(200, 135, 74, 0.0)' },
            ]),
          },
        },
        {
          name: 'Постоянные', type: 'line', smooth: true, symbol: 'circle', symbolSize: 8, data: regular,
          lineStyle: { width: 3, color: '#e0b78a' },
          itemStyle: { color: '#e0b78a', borderColor: 'rgba(0,0,0,0.5)', borderWidth: 2 },
          areaStyle: {
            color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
              { offset: 0, color: 'rgba(224, 183, 138, 0.3)' }, { offset: 1, color: 'rgba(224, 183, 138, 0.0)' },
            ]),
          },
        },
      ],
    })
  }

  if (hallEl.value && !hallChart) {
    hallChart = echarts.init(hallEl.value, null, { renderer: 'canvas' })
    const halls = ['C1', 'B1', 'A1', 'B2']
    const load = [42, 58, 71, 86]
    hallChart.setOption({
      textStyle: BASE_TEXT,
      grid: { top: 10, right: 40, bottom: 10, left: 45 },
      tooltip: { ...TOOLTIP, trigger: 'axis', axisPointer: { type: 'shadow' } },
      xAxis: {
        type: 'value', axisLine: { show: false }, axisTick: { show: false }, splitLine: SPLIT_LINE,
        axisLabel: { color: 'rgba(244, 236, 223, 0.7)', fontSize: 13, formatter: '{value}%', max: 100 },
      },
      yAxis: {
        type: 'category', data: halls, axisLine: AXIS_LINE, axisTick: { show: false },
        axisLabel: { color: 'rgba(244, 236, 223, 0.9)', fontFamily: 'IBM Plex Mono, monospace', fontSize: 14 },
      },
      series: [{
        type: 'bar', data: load, barWidth: 18,
        itemStyle: {
          color: new echarts.graphic.LinearGradient(0, 0, 1, 0, [
            { offset: 0, color: '#6b4423' }, { offset: 1, color: '#c8874a' },
          ]),
          borderRadius: [0, 6, 6, 0],
        },
        label: { show: true, position: 'right', color: 'rgba(244, 236, 223, 0.95)', fontSize: 13, formatter: '{c}%' },
      }],
    })
  }
}

function resizeCharts() {
  donutChart?.resize()
  barChart?.resize()
  lineChart?.resize()
  hallChart?.resize()
}

onMounted(() => {
  if (typeof IntersectionObserver === 'undefined') {
    visible.value = true
    nextTick(() => initCharts())
  } else {
    observer = new IntersectionObserver(
      async (entries) => {
        for (const entry of entries) {
          if (entry.isIntersecting && entry.intersectionRatio >= 0.2) {
            if (visible.value) return
            await nextTick()
            visible.value = true
          }
        }
      },
      { threshold: [0, 0.2, 0.5] }
    )
    if (root.value) observer.observe(root.value)
  }

  if (typeof ResizeObserver !== 'undefined' && root.value) {
    resizeObs = new ResizeObserver(() => {
      if (visible.value) resizeCharts()
    })
    resizeObs.observe(root.value)
  }

  window.addEventListener('resize', () => {
    if (visible.value) resizeCharts()
  })
})

onBeforeUnmount(() => {
  if (observer && root.value) observer.unobserve(root.value)
  observer = null
  if (resizeObs) { resizeObs.disconnect(); resizeObs = null }
  donutChart?.dispose()
  barChart?.dispose()
  lineChart?.dispose()
  hallChart?.dispose()
  donutChart = barChart = lineChart = hallChart = null
})

watch(visible, (v) => {
  if (v) {
    nextTick(() => {
      initCharts()
      requestAnimationFrame(() => resizeCharts())
    })
  }
})
</script>

<style scoped lang="scss">
@use "../styles/variables" as *;

$text:        #f4ecdf;
$muted:       rgba(244, 236, 223, 0.85);
$muted-2:     rgba(244, 236, 223, 0.65);
$paper:       #ede0c8;
$accent:      #c8874a;
$accent-soft: #e0b78a;

$mono: "IBM Plex Mono", "JetBrains Mono", ui-monospace, SFMono-Regular, Menlo, Consolas, monospace;
$ease-soft: cubic-bezier(0.25, 0.46, 0.45, 0.94);

@keyframes fade-in {
  from { opacity: 0; transform: translateY(10px); }
  to   { opacity: 1; transform: translateY(0); }
}

.crm {
  position: relative;
  display: flex;
  flex-direction: column;

  width: 100%;
  height: 100%;

  min-height: 0;

  padding: 24px 32px;
  color: $text;

  overflow: hidden;

  background: rgba(0, 0, 0, 0.55);
  backdrop-filter: blur(24px);
  -webkit-backdrop-filter: blur(24px);
  border-radius: 16px;

  box-sizing: border-box;

  &__stage {
    position: relative;
    z-index: 1;

    flex: 1;
    min-height: 0;

    display: grid;
    grid-template-columns: 340px 1fr;
    gap: 20px;

    height: 100%;
  }
}

.stage__left {
  display: flex;
  flex-direction: column;
  min-height: 0;
}

.stage__right {
  display: flex;
  flex-direction: column;
  gap: 20px;
  min-height: 0;
}

/* Метка раздела */
.section-label {
  font-family: $mono;
  font-size: 0.85rem;
  font-weight: 600;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: $muted-2;
  margin-bottom: 12px;
  padding-left: 4px;
  opacity: 0;
  .crm.is-visible & { animation: fade-in 0.8s $ease-soft 0.1s both; }
}

/* --- KPI --- */
.kpi {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 16px;
  flex: 0 0 auto;

  &__card {
    display: flex;
    flex-direction: column;
    gap: 8px;
    padding: 18px 20px;
    background-color: rgba(255, 255, 255, 0.06);
    border: 1px solid rgba(200, 170, 135, 0.15);
    border-radius: 12px;
    opacity: 0;
    .crm.is-visible & {
      animation: fade-in 0.8s $ease-soft both;
      animation-delay: calc(0.1s + var(--i) * 0.08s);
    }
  }

  &__label {
    font-family: $mono;
    font-size: 0.85rem;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: $muted-2;
  }

  &__value {
    font-family: Georgia, "Times New Roman", serif;
    font-size: 1.65rem;
    font-weight: 600;
    color: $paper;
    line-height: 1.1;
  }

  &__delta {
    font-family: $mono;
    font-size: 0.85rem;
    font-weight: 600;
    letter-spacing: 0.05em;
    &--up   { color: #d5e2a4; }
    &--down { color: #e0a89a; }
  }
}

/* --- Графики --- */
.charts-row {
  display: grid;
  grid-template-columns: 1fr 1.2fr;
  gap: 20px;
  flex: 1;
  min-height: 0;
}

.bottom-row {
  display: grid;
  grid-template-columns: 1fr 1.5fr;
  gap: 20px;
  flex: 0 0 auto;
}

.chart {
  display: flex;
  flex-direction: column;
  padding: 20px;
  background-color: rgba(255, 255, 255, 0.06);
  border: 1px solid rgba(200, 170, 135, 0.15);
  border-radius: 12px;
  min-height: 0;
  opacity: 0;
  .crm.is-visible & { animation: fade-in 0.8s $ease-soft 0.3s both; }

  &--donut {
    flex: 1;
    min-height: 0;
    .crm.is-visible & { animation-delay: 0.2s; }
  }

  &__head {
    display: flex;
    flex-direction: column;
    gap: 4px;
    flex: 0 0 auto;
    margin-bottom: 12px;
  }

  &__title {
    font-size: 1.15rem;
    font-weight: 600;
    color: $paper;
    letter-spacing: -0.01em;
  }

  &__sub {
    font-family: $mono;
    font-size: 0.8rem;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: $muted-2;
  }

  &__body {
    position: relative;
    flex: 1;
    min-height: 0;
    display: flex;
    align-items: stretch;
    gap: 20px;
  }

  &__canvas {
    flex: 1;
    min-width: 0;
    min-height: 0;
  }
}

.chart--donut .chart__body {
  flex-direction: column;
  align-items: center;
  gap: 16px;
}

.chart--donut .chart__canvas {
  flex: 1;
  width: 100%;
}

/* --- Легенда --- */
.legend {
  width: 100%;
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: column;
  gap: 10px;

  &__row {
    display: grid;
    grid-template-columns: 14px 1fr auto;
    align-items: center;
    gap: 12px;
    font-size: 0.95rem;
    color: $muted;
    padding: 8px 12px;
    background: rgba(0, 0, 0, 0.2);
    border-radius: 8px;
  }

  &__dot { width: 14px; height: 14px; border-radius: 4px; }
  &__name { color: rgba(244, 236, 223, 0.95); font-weight: 500; }
  &__val {
    font-family: $mono;
    font-size: 0.95rem;
    font-weight: 600;
    color: $paper;
  }
}

/* --- Боты --- */
.bots {
  display: flex;
  flex-direction: column;
  gap: 12px;
  min-width: 0;
}

.bots__head { margin-bottom: 4px; }
.bots__label {
  font-family: $mono;
  font-size: 0.85rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: $muted-2;
}

.bots__grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
}

.bot {
  display: flex;
  align-items: flex-start;
  gap: 14px;
  padding: 16px;
  background-color: rgba(255, 255, 255, 0.06);
  border: 1px solid rgba(200, 170, 135, 0.15);
  border-radius: 12px;
  min-width: 0;
  opacity: 0;
  .crm.is-visible & { animation: fade-in 0.8s $ease-soft 0.5s both; }

  &__icon {
    flex: 0 0 auto;
    display: grid;
    place-items: center;
    width: 42px;
    height: 42px;
    color: $paper;
    background-color: rgba(200, 135, 74, 0.15);
    border-radius: 10px;
  }
  &--tg &__icon { background-color: rgba(64, 130, 180, 0.2); color: #a8cbe0; }
  &--vk &__icon { background-color: rgba(70, 110, 160, 0.2); color: #a8bcd8; }
  &--total &__icon { background-color: rgba(200, 135, 74, 0.2); color: $accent-soft; }

  &__icon-glyph { font-family: $mono; font-size: 1.3rem; font-weight: 700; }

  &__body {
    display: flex;
    flex-direction: column;
    gap: 6px;
    min-width: 0;
    flex: 1;
  }

  &__name {
    font-size: 1.05rem;
    font-weight: 600;
    color: $paper;
  }

  &__metrics {
    list-style: none;
    margin: 0;
    padding: 0;
    display: flex;
    flex-direction: column;
    gap: 4px;
    margin-top: 4px;

    li {
      display: flex;
      justify-content: space-between;
      gap: 10px;
      font-size: 0.85rem;
      color: $muted;
      b {
        font-family: $mono;
        font-weight: 600;
        color: $paper;
      }
    }
  }
}

/* ==========================================================================
   ПЛАНШЕТ / УЗКИЙ ДЕСКТОП
   ========================================================================== */

@media (max-width: 1200px) {
  .crm {
    padding: 20px 22px;
  }

  .crm__stage {
    grid-template-columns: 1fr;
    grid-template-rows: auto auto;

    overflow-y: auto;
    overscroll-behavior: auto;
    -webkit-overflow-scrolling: touch;

    scrollbar-width: none;
    &::-webkit-scrollbar { display: none; }
  }

  .stage__left { height: auto; }
  .stage__right { height: auto; }

  .chart--donut {
    min-height: 300px;
  }

  .charts-row,
  .bottom-row {
    grid-template-columns: 1fr;
    flex: 0 0 auto;
  }

  .charts-row .chart { min-height: 240px; }
  .bottom-row .chart { min-height: 200px; }

  .bots__grid {
    grid-template-columns: 1fr;
  }
}

/* ==========================================================================
   МОБИЛЬНАЯ ВЕРСИЯ
   ========================================================================== */

@media (max-width: 768px) {
  .crm {
    padding: 12px 14px;
    border-radius: 12px;
  }

  .crm__stage {
    gap: 10px;
  }

  .section-label {
    font-size: 0.7rem;
    margin-bottom: 8px;
  }

  /* KPI — 2×2 */
  .kpi {
    grid-template-columns: 1fr 1fr;
    gap: 10px;
  }

  .kpi__card {
    padding: 12px 14px;
    gap: 4px;
  }

  .kpi__label { font-size: 0.65rem; letter-spacing: 0.08em; }
  .kpi__value { font-size: 1.15rem; }
  .kpi__delta { font-size: 0.7rem; }

  /* Графики */
  .stage__right { gap: 10px; }

  .charts-row,
  .bottom-row { gap: 10px; }

  .chart {
    padding: 12px;
    border-radius: 10px;
  }

  .chart__head { margin-bottom: 6px; }
  .chart__title { font-size: 0.9rem; }
  .chart__sub   { font-size: 0.6rem; letter-spacing: 0.08em; }

  /* Donut — компактнее, только как декор */
  .chart--donut {
    min-height: 180px;
    padding: 12px;
  }

  .chart--donut .chart__body {
    gap: 0;
  }

  .chart--donut .chart__canvas {
    flex: 0 0 140px;
    max-width: 140px;
  }

  /* Легенду прячем — данные уже есть в KPI */
  .legend { display: none; }

  .charts-row .chart { min-height: 170px; }
  .bottom-row .chart { min-height: 150px; }

  /* Боты — компактно */
  .bots { gap: 8px; }
  .bots__label { font-size: 0.7rem; letter-spacing: 0.1em; }

  .bots__grid { gap: 8px; }

  .bot {
    padding: 10px 12px;
    gap: 10px;
    border-radius: 10px;
  }

  .bot__icon { width: 34px; height: 34px; border-radius: 8px; }
  .bot__icon-glyph { font-size: 1.1rem; }
  .bot__name { font-size: 0.9rem; }
  .bot__metrics li { font-size: 0.75rem; gap: 6px; }
  .bot__metrics li b { font-size: 0.75rem; }
}

@media (max-width: 400px) {
  .crm { padding: 10px 12px; }

  .kpi__value { font-size: 1rem; }
  .kpi__label { font-size: 0.6rem; }

  .chart { padding: 12px; }
  .chart__title { font-size: 0.85rem; }

  .chart--donut { min-height: 160px; }
  .chart--donut .chart__canvas {
    flex: 0 0 120px;
    max-width: 120px;
  }
  .charts-row .chart { min-height: 160px; }
  .bottom-row .chart { min-height: 140px; }
}
</style>