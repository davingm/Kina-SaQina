<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'

const characterRef = ref<HTMLElement | null>(null)   // takina_hero.png（最终层，最右侧）
const sc1Ref       = ref<HTMLElement | null>(null)   // takina_sc.png — 最左侧（偏移 -3）
const sc2Ref       = ref<HTMLElement | null>(null)   // takina_sc.png — 中间（偏移 -2）
const sc3Ref       = ref<HTMLElement | null>(null)   // takina_sc.png — 最靠近主图（偏移 -1）
const infoCardRef  = ref<HTMLElement | null>(null)
const watermarkRef = ref<HTMLElement | null>(null)
const subTextRef   = ref<HTMLElement | null>(null)
const yellowRef    = ref<HTMLElement | null>(null)

// 每层偏移量：每张草稿图相对于下一层向左偏移 72px
// sc3 = -72px（相对主图），sc2 = -144px，sc1 = -216px
const OFFSET = 72

onMounted(() => {
  const tl = gsap.timeline({ defaults: { ease: 'power3.out' } })

  // ── 设置初始状态（所有元素从屏幕左侧外部进入）──
  gsap.set([sc1Ref.value, sc2Ref.value, sc3Ref.value, characterRef.value], {
    x: '-150%',
    opacity: 0,
  })
  gsap.set(infoCardRef.value,  { x: -60, opacity: 0 })
  gsap.set(watermarkRef.value, { y: 40,  opacity: 0 })
  gsap.set(subTextRef.value,   { x: -30, opacity: 0 })
  gsap.set(yellowRef.value,    { scaleX: 0, transformOrigin: 'right center' })

  // ── 时间轴 ──
  tl
    // 1. 黄色色块从右侧展开
    .to(yellowRef.value, { scaleX: 1, duration: 0.65, ease: 'power4.inOut' })

    // 2. sc1（最左侧）滑入至最终位置
    .to(sc1Ref.value, {
      x: -(OFFSET * 3),   // -216px，相对于主图位置（right:0）
      opacity: 0.55,
      duration: 0.55,
      ease: 'power2.out',
    }, '-=0.15')

    // 3. sc2 滑入
    .to(sc2Ref.value, {
      x: -(OFFSET * 2),   // -144px
      opacity: 0.65,
      duration: 0.5,
      ease: 'power2.out',
    }, '-=0.3')

    // 4. sc3 滑入
    .to(sc3Ref.value, {
      x: -OFFSET,          // -72px
      opacity: 0.75,
      duration: 0.5,
      ease: 'power2.out',
    }, '-=0.3')

    // 5. 主图滑入至最右侧位置（x:0）
    .to(characterRef.value, {
      x: 0,
      opacity: 1,
      duration: 0.65,
      ease: 'power3.out',
    }, '-=0.25')

    // 6. 信息卡片 + 副标题 + 水印同时显现
    .to(infoCardRef.value,  { x: 0, opacity: 1, duration: 0.55 }, '-=0.45')
    .to(subTextRef.value,   { x: 0, opacity: 1, duration: 0.45 }, '-=0.4')
    .to(watermarkRef.value, { y: 0, opacity: 1, duration: 0.65, ease: 'power2.out' }, '-=0.45')
})
</script>

<template>
  <section class="hero" id="hero-section">
    <!-- 左上角斜线装饰 -->
    <div class="deco-diagonal deco-diagonal--top"></div>

    <!-- 信息卡片（左上角）-->
    <div class="info-card" ref="infoCardRef">
      <div class="info-card__row info-card__row--top">
        <div class="info-card__title-wrap">
          <span class="bracket">[</span>
          <span class="info-card__title">INOUE TAKINA</span>
          <span class="bracket">]</span>
        </div>
        <div class="info-card__desc">
          <span>LYCORIS RECOIL AGENT</span>
          <span>DA OPERATIVE · LilyBell</span>
        </div>
      </div>
      <div class="info-card__row info-card__row--meta">
        <span class="info-card__name">Inoue Takina</span>
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

    <!-- 副标题文字 -->
    <p class="hero__sub-text" ref="subTextRef">DA OPERATIVE | Lycoris Recoil</p>

    <!-- 大型斜线填充水印 -->
    <div class="hero__watermark" aria-hidden="true" ref="watermarkRef">TAKINA</div>

    <!-- 右侧黄色色块 -->
    <div class="hero__yellow-block" ref="yellowRef"></div>

    <!--
      角色图层 — 全部叠放于右下角。
      sc1（最左侧，最先出现）→ sc2 → sc3 → 主图（最右侧，最后出现）
      每层最终偏移量通过 GSAP x: -(OFFSET * n) 控制
    -->
    <!-- 草稿图层 1 — 最左侧 -->
    <div class="hero__character hero__character--sc" ref="sc1Ref">
      <img src="/kina/takina_sc.png" alt="" aria-hidden="true" draggable="false" />
    </div>
    <!-- 草稿图层 2 -->
    <div class="hero__character hero__character--sc" ref="sc2Ref">
      <img src="/kina/takina_sc.png" alt="" aria-hidden="true" draggable="false" />
    </div>
    <!-- 草稿图层 3 — 最靠近主图 -->
    <div class="hero__character hero__character--sc" ref="sc3Ref">
      <img src="/kina/takina_sc.png" alt="" aria-hidden="true" draggable="false" />
    </div>
    <!-- 主图 — 锚定右侧，最后出现 -->
    <div class="hero__character" ref="characterRef">
      <img src="/kina/takina_hero.png" alt="Inoue Takina" draggable="false" />
    </div>

    <!-- 十字标记 -->
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

  // ── 角色图片 ──
  &__character {
    position: absolute;
    right: 0;
    bottom: 0;
    z-index: 5;
    display: flex;
    align-items: flex-end;
    justify-content: flex-end;
    pointer-events: none;
    will-change: transform;

    img {
      display: block;
      // 按原始尺寸渲染；高度限制为 hero 区域高度，防止垂直溢出
      height: 100%;
      max-height: 420px;
      width: auto;
      object-fit: contain;
      object-position: bottom right;
      user-select: none;
    }

    // 草稿图层 — 位于主图后方，透明度更低 + 轻微去饱和
    &--sc {
      z-index: 4;

      img {
        // 与主图保持相同尺寸
        max-height: 420px;
        // 草稿透明度通过 GSAP opacity 自然呈现，
        // 额外添加滤镜以营造"残影"效果
        filter: grayscale(30%) brightness(1.05);
      }
    }
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

  /* ── 斜线填充水印 ── */
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

    // 斜线/网格填充效果
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

// ── 斜线装饰 ──
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

// ── 信息卡片 ──
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

// ── 点阵图标 ──
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

// ── 十字标记 ──
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

// ── 响应式 ──
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
    &__character img {
      max-height: 320px;
    }
    &__character--sc img {
      max-height: 320px;
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
    &__character img {
      max-height: 260px;
    }
    &__character--sc img {
      max-height: 260px;
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
