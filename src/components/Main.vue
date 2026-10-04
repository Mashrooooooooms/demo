<template>
  <div class="main">
    <header class="main__header">
      <p class="main__note">Демонстрационный материал, все совпадения случайны</p>
      <h1 class="main__title">Main</h1>
    </header>

    <main class="main__content">
        <BlockZero/>
      <BlockOne />
      <BlockTwo />
      <BlockThree />
      <BlockFour />
      <BlockFive />
      <BlockSix />
    </main>

    <footer class="main__footer">
      <small>© 2026</small>
    </footer>
  </div>
</template>

<script setup>
/**
 * main.vue
 * .main__content — grid-контейнер со scroll-snap.
 * grid-auto-rows: 100% делает каждую секцию ровно в высоту контейнера,
 * поэтому внутри блока можно смело использовать height: 100% и %-высоты.
 */

import BlockZero from "./0.vue"
import BlockOne   from "./1.vue";
import BlockThree   from "./2.vue";
import BlockTwo from "./3.vue";
import BlockFour  from "./4.vue";
import BlockFive  from "./5.vue";
import BlockSix from "./6.vue"
</script>

<style scoped lang="scss">
@use "../styles/variables" as *;

/* ==========================================================================
   ЛОКАЛЬНЫЕ ПЕРЕМЕННЫЕ MAIN
   ========================================================================== */

$note-size:      0.6875rem;
$note-weight:    400;
$note-spacing:   0.08em;
$note-leading:   1.4;
$note-color:     rgba(255, 255, 255, 0.75);
$note-max-width: 22rem;

$note-bg:        rgba(255, 255, 255, 0.08);
$note-blur:      8px;
$note-padding-y: 6px;
$note-padding-x: 12px;
$note-radius:    6px;

/* ==========================================================================
   СТИЛИ
   ========================================================================== */

.main {
  width: $size-full;
  max-width: $size-full;
  min-height: $viewport-height;
  min-height: $viewport-height-dynamic;

  display: flex;
  flex-direction: column;

  background-color: $color-bg;
  background-image: $bg-image;
  background-size: $bg-size;
  background-position: $bg-position;
  background-repeat: $bg-repeat;

  color: $color-text;

  padding-top:    env(safe-area-inset-top,    $safe-area-fallback);
  padding-right:  env(safe-area-inset-right,  $safe-area-fallback);
  padding-bottom: env(safe-area-inset-bottom, $safe-area-fallback);
  padding-left:   env(safe-area-inset-left,   $safe-area-fallback);

  overflow: $overflow-hidden;

  &__header,
  &__footer {
    flex: $flex-none;
    display: flex;
    align-items: center;
    padding: $space-sm $space-md;
  }

  &__header {
    justify-content: space-between;
    gap: $space-md;
    border-bottom: $border-width $border-style $color-border;
  }

  &__footer {
    justify-content: center;
    border-top: $border-width $border-style $color-border;
    color: $color-muted;
  }

  &__title {
    font-size: $font-size-title;
    font-weight: $font-weight-title;
  }

  &__note {
    max-width: $note-max-width;

    font-size: $note-size;
    font-weight: $note-weight;
    letter-spacing: $note-spacing;
    line-height: $note-leading;
    color: $note-color;

    text-align: left;

    background-color: $note-bg;
    backdrop-filter: blur($note-blur);
    -webkit-backdrop-filter: blur($note-blur);

    padding: $note-padding-y $note-padding-x;
    border-radius: $note-radius;
  }

  &__content {
    flex: $flex-fill;
    min-height: $size-zero;

    display: grid;
    grid-auto-flow: row;
    grid-auto-rows: $size-full;

    overflow-y: $overflow-y;
    -webkit-overflow-scrolling: $scroll-touch;
    overscroll-behavior: $overscroll;

    scroll-snap-type: $snap-type;

    scrollbar-width: none;
    &::-webkit-scrollbar {
      display: none;
    }

    padding: $size-zero;

    > * {
      scroll-snap-align: $snap-align;
      scroll-snap-stop: $snap-stop;
    }
  }
}
</style>