<script setup lang="ts">
// Page Footer — Organization branding, diagonal decoration
</script>

<template>
  <footer class="footer" id="footer-section">
    <!-- Diagonal Decoration Bottom-Left -->
    <div class="deco-diagonal deco-diagonal--bottom"></div>

    <!-- Footer Logo -->
    <div class="footer__logo">
      <svg width="48" height="48" viewBox="0 0 48 48" fill="none">
        <polygon points="24,4 44,40 4,40" fill="#FFD600" opacity="0.9"/>
        <polygon points="24,12 36,36 12,36" fill="#E8456B" opacity="0.7"/>
        <line x1="24" y1="4" x2="24" y2="40" stroke="#FFD600" stroke-width="2"/>
      </svg>
    </div>

    <!-- Footer Content -->
    <div class="footer__content">
      <span class="footer__org">BITNP:Net Pioneer Association of BIT</span>
      <h2 class="footer__title">KINA SAQINA</h2>
      <span class="footer__subtitle">THE KINA SAQINA IS THE KINA SAQINA | BITNP</span>
    </div>
  </footer>
</template>

<style scoped lang="scss">
.footer {
  position: relative;
  width: 100%;
  display: flex;
  align-items: center;
  gap: 20px;
  padding: 24px 40px 24px 180px;
  background: var(--dark);
  min-height: 88px;
  overflow: hidden;

  &__logo {
    position: relative;
    z-index: 10;
    flex-shrink: 0;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  &__content {
    position: relative;
    z-index: 10;
    display: flex;
    flex-direction: column;
    gap: 2px;
  }

  &__org {
    font-family: var(--font-en);
    font-size: 10px;
    font-weight: 500;
    color: rgba(255, 255, 255, 0.5);
    letter-spacing: 1.5px;
    text-transform: uppercase;
  }

  &__title {
    font-family: var(--font-en);
    font-size: 28px;
    font-weight: 900;
    color: var(--white);
    letter-spacing: 4px;
    margin: 0;
    line-height: 1.2;
  }

  &__subtitle {
    font-family: var(--font-en);
    font-size: 8px;
    color: rgba(255, 255, 255, 0.3);
    letter-spacing: 1px;
    text-transform: uppercase;
  }
}

// ── Diagonal Decoration ──
.deco-diagonal {
  position: absolute;
  z-index: 15;
  pointer-events: none;

  &--bottom {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 120px;
    height: 100%;
    background: repeating-linear-gradient(
      -55deg,
      var(--yellow) 0,
      var(--yellow) 1.5px,
      transparent 1.5px,
      transparent 9px
    );
    opacity: 0.6;
  }
}

// ── Responsive ──
@media (max-width: 900px) {
  .footer {
    padding-left: 100px;
  }
}

@media (max-width: 600px) {
  .footer {
    padding: 20px 16px 20px 80px;

    &__title { font-size: 20px; }
  }

  .deco-diagonal--bottom { width: 60px; }
}
</style>
