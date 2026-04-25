<script setup lang="ts">
// Hero Section — Info card, hatched watermark, yellow block
</script>

<template>
  <section class="hero" id="hero-section">
    <!-- Diagonal Decoration Top-Left -->
    <div class="deco-diagonal deco-diagonal--top"></div>

    <!-- Info Card (Top-Left) -->
    <div class="info-card">
      <div class="info-card__row info-card__row--top">
        <div class="info-card__title-wrap">
          <span class="bracket">[</span>
          <span class="info-card__title">KINA SAQINA</span>
          <span class="bracket">]</span>
        </div>
        <div class="info-card__desc">
          <span>THE PIONEER'S MASCOT FOR</span>
          <span>THE KINA SAQINA PROJECT...</span>
        </div>
      </div>
      <div class="info-card__row info-card__row--meta">
        <span class="info-card__name">Kina SaQina</span>
        <span class="info-card__fraction">1/1</span>
      </div>
      <div class="info-card__icons">
        <div class="berry-dot-icon" v-for="n in 6" :key="n">
          <span></span><span></span><span></span>
          <span></span><span></span><span></span>
          <span></span><span></span><span></span>
        </div>
      </div>
    </div>

    <!-- Watermark Sub Text -->
    <p class="hero__sub-text">THE KINA SAQINA IS THE KINA SAQINA | BITNP</p>

    <!-- Large Hatched Watermark -->
    <div class="hero__watermark" aria-hidden="true">KINASAQIN</div>

    <!-- Yellow Block (Right Side) -->
    <div class="hero__yellow-block"></div>

    <!-- Cross Marks -->
    <div class="cross-mark cross-mark--1">+</div>
    <div class="cross-mark cross-mark--2">+</div>
  </section>
</template>

<style scoped lang="scss">
.hero {
  position: relative;
  width: 100%;
  height: 420px;
  display: flex;
  align-items: flex-start;
  overflow: hidden;

  &__yellow-block {
    position: absolute;
    top: 0;
    right: 0;
    width: 44%;
    height: 100%;
    background: var(--yellow);
    z-index: 1;
  }

  &__sub-text {
    position: absolute;
    z-index: 10;
    top: 200px;
    left: 48px;
    font-family: var(--font-en);
    font-size: 10px;
    letter-spacing: 2px;
    color: var(--gray-mid);
    text-transform: uppercase;
  }

  /* ── HATCHED / ARSIR WATERMARK ── */
  &__watermark {
    position: absolute;
    z-index: 2;
    bottom: 20px;
    left: 30px;
    font-family: var(--font-en);
    font-size: clamp(100px, 14vw, 180px);
    font-weight: 900;
    letter-spacing: 8px;
    text-transform: uppercase;
    line-height: 1;
    white-space: nowrap;
    user-select: none;
    pointer-events: none;

    // Arsir / Hatching fill effect
    background: repeating-linear-gradient(
      -45deg,
      rgba(0, 0, 0, 0.18) 0px,
      rgba(0, 0, 0, 0.18) 2.5px,
      rgba(0, 0, 0, 0.04) 2.5px,
      rgba(0, 0, 0, 0.04) 6px
    );
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent;
    -webkit-text-stroke: 1px rgba(0, 0, 0, 0.06);
  }
}

// ── Diagonal Decoration ──
.deco-diagonal {
  position: absolute;
  z-index: 15;
  pointer-events: none;

  &--top {
    top: 0;
    left: 0;
    width: 140px;
    height: 200px;
    background: repeating-linear-gradient(
      -55deg,
      var(--yellow) 0,
      var(--yellow) 1.5px,
      transparent 1.5px,
      transparent 9px
    );
    opacity: 0.7;
  }
}

// ── Info Card ──
.info-card {
  position: relative;
  z-index: 10;
  margin-top: 32px;
  margin-left: 48px;
  border: 1.5px solid var(--dark);
  padding: 16px 20px;
  background: var(--white);
  max-width: 420px;

  &__row {
    display: flex;
    align-items: baseline;
    gap: 12px;

    &--top { margin-bottom: 6px; }
    &--meta { margin-bottom: 12px; }
  }

  &__title-wrap {
    display: flex;
    align-items: baseline;
    gap: 6px;
    flex-shrink: 0;
  }

  &__title {
    font-family: var(--font-en);
    font-weight: 800;
    font-size: 18px;
    letter-spacing: 1.5px;
    color: var(--dark);
  }

  &__desc {
    display: flex;
    flex-direction: column;
    gap: 1px;
    font-family: var(--font-en);
    font-size: 8px;
    color: var(--gray-mid);
    letter-spacing: 0.5px;
    line-height: 1.3;
    text-transform: uppercase;
  }

  &__name {
    font-family: var(--font-en);
    font-size: 14px;
    font-weight: 500;
    color: var(--text-dark);
    letter-spacing: 0.5px;
  }

  &__fraction {
    font-family: var(--font-en);
    font-size: 13px;
    font-weight: 400;
    color: var(--gray-mid);
    margin-left: 8px;
  }

  &__icons {
    display: flex;
    gap: 8px;
    flex-wrap: wrap;
  }
}

.bracket {
  font-family: var(--font-en);
  font-weight: 300;
  font-size: 18px;
  color: var(--dark);
}

// ── Berry Dot Icons ──
.berry-dot-icon {
  display: grid;
  grid-template-columns: repeat(3, 5px);
  grid-template-rows: repeat(3, 5px);
  gap: 2px;
  width: 19px;
  height: 19px;

  span {
    background: var(--dark);
    border-radius: 50%;
    width: 5px;
    height: 5px;
  }
}

// ── Cross Marks ──
.cross-mark {
  position: absolute;
  font-family: var(--font-en);
  font-size: 14px;
  font-weight: 300;
  color: #ccc;
  z-index: 5;
  user-select: none;
  pointer-events: none;

  &--1 { top: 200px; left: 160px; }
  &--2 { top: 50px; right: 46%; }
}

// ── Responsive ──
@media (max-width: 900px) {
  .hero {
    height: 320px;

    &__yellow-block { width: 35%; }
    &__watermark {
      font-size: 80px;
      bottom: 10px;
      left: 16px;
    }
    &__sub-text {
      left: 24px;
      top: 180px;
    }
  }

  .info-card {
    margin-left: 24px;
    margin-top: 24px;
    max-width: 320px;
    padding: 12px 16px;
  }

  .deco-diagonal--top {
    width: 80px;
    height: 120px;
  }
}

@media (max-width: 600px) {
  .hero {
    height: 260px;

    &__watermark {
      font-size: 50px;
      -webkit-text-stroke: 1px rgba(0, 0, 0, 0.04);
    }
    &__sub-text {
      font-size: 8px;
      left: 16px;
      top: 155px;
    }
  }

  .info-card {
    margin-left: 16px;
    margin-top: 16px;
    max-width: 260px;
    padding: 10px 12px;

    &__title { font-size: 14px; }
    &__desc { display: none; }
  }

  .deco-diagonal--top {
    width: 50px;
    height: 80px;
  }
}
</style>
