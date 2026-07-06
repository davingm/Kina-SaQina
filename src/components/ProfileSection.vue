<script setup lang="ts">
// 个人资料区 — 角色名称、标签、描述、3D 模型区域
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'

const iconWrapRef = ref<HTMLElement | null>(null)
const nameRef     = ref<HTMLElement | null>(null)

onMounted(() => {
  // ── 1. 图标：如时钟指针般揭示（顺时针擦除，via clip-path）
  //
  // 原理：使用 conic-gradient 作为 CSS mask 遮罩，模拟时钟扫描效果。
  // 从 7 点方向（210°）开始，顺时针扫过 360°，逐步显现图标。

  const iconEl = iconWrapRef.value
  if (iconEl) {
    // 初始状态：遮罩完全覆盖（显示角度为 0°）
    const obj = { angle: 0 }

    // 设置初始 mask：全部遮盖
    // conic-gradient：white = 显现区域，transparent = 遮盖区域
    // 从 7 点方向（210°）开始，初始扫过宽度为 0
    const updateMask = (angleDeg: number) => {
      const start = 210
      if (angleDeg >= 360) {
        // 完全显现 — 移除 mask
        iconEl.style.webkitMaskImage = 'none'
        iconEl.style.maskImage       = 'none'
      } else {
        const mask = `conic-gradient(from ${start}deg, white 0deg ${angleDeg}deg, transparent ${angleDeg}deg 360deg)`
        iconEl.style.webkitMaskImage = mask
        iconEl.style.maskImage       = mask
      }
    }

    updateMask(0)

    gsap.to(obj, {
      angle: 360,
      duration: 1.2,
      ease: 'power2.inOut',
      delay: 0.15,
      onUpdate() { updateMask(obj.angle) },
    })
  }

  // ── 2. 括号展开：[] → [  ] → [井ノ上 瀧奈]
  //
  // 策略：将名称包裹在 width: 0、overflow: hidden 的容器中。
  // 左右括号位置不变 — 名称容器从 width 0 展开至自然宽度，
  // 视觉上如同括号被"撑开"。名称本身同步淡入。

  const nameEl = nameRef.value
  if (nameEl) {
    // 先测量名称的自然宽度，再从 0 开始动画
    const naturalWidth = nameEl.scrollWidth
    gsap.set(nameEl, { width: 0, opacity: 0, overflow: 'hidden', whiteSpace: 'nowrap' })

    gsap.timeline({ delay: 0.4 })
      .to(nameEl, {
        width: naturalWidth,
        duration: 0.85,
        ease: 'power3.inOut',
      })
      .to(nameEl, {
        opacity: 1,
        duration: 0.45,
        ease: 'power2.out',
      }, '-=0.65') // 括号刚开始展开时名称开始淡入
  }
})
</script>

<template>
  <section class="profile" id="profile-section">
    <div class="profile__left">
      <!-- 角色名称 -->
      <div class="profile__name-row">
        <div class="berry-accent" ref="iconWrapRef">
          <img src="/ryco.ico" alt="Lycoris Recoil" />
        </div>
        <span class="bracket bracket--lg">[</span>
        <h1 class="profile__name" ref="nameRef">井ノ上 瀧奈</h1>
        <span class="bracket bracket--lg">]</span>
      </div>

      <!-- 标签网格 -->
      <div class="tags">
        <div class="tags__row">
          <div class="tag-group">
            <span class="tag-label">作者</span>
            <span class="tag-value">Kin · davingm</span>
          </div>
          <div class="tag-group">
            <span class="tag-label">种族</span>
            <span class="tag-value">人类·特工</span>
          </div>
        </div>
        <div class="tags__row">
          <div class="tag-group">
            <span class="tag-label">日文</span>
            <span class="tag-value">井ノ上 瀧奈</span>
          </div>
          <div class="tag-group">
            <span class="tag-label">英文</span>
            <span class="tag-value">Inoue Takina</span>
          </div>
        </div>
      </div>

      <!-- 青色强调线 -->
      <div class="teal-line"></div>

      <!-- 角色描述 -->
      <div class="profile__desc">
        <p>
          绮娜醒来时，发现自己又一次卡在同一个控制面板里。
          屏幕上的年份不断闪烁——1998、2003、1996……又回来了。

          "不会吧……"她低声嘀咕。

          她揉了揉眼睛，下意识地点下了"时间重新同步"。
          这是她第一百四十三次做这个动作了。

          系统恢复正常，世界看起来一切如常。

          ……至少表面上是这样。

          绮娜盯着屏幕，比平时多看了一会儿。
          她知道，这不只是普通的错误。

          不过也无所谓——
          这种事情，从来都不是免费的。
          总是要付出代价的。
        </p>
        <p class="profile__desc-sub">
          画面闪烁了一下，恢复了。
        </p>
        <p class="profile__desc-note">
          古灵精怪 —— 一指期限制与亮度平衡至宝 <span class="dot-sep">·</span> 道美妆纷纷仿扮精计 <span class="highlight-red">* 红</span>
        </p>
      </div>
    </div>

    <!-- 右侧（3D 模型区域）-->
    <div class="profile__right">
      <div class="model-placeholder">
        <!-- 3D 模型区域 — 将由 Three.js 驱动 -->
      </div>
      <button class="btn-3d" id="btn-3d-toggle" aria-label="Toggle 3D View">
        <span class="btn-3d__icon">3D</span>
      </button>
    </div>
  </section>
</template>

<style scoped lang="scss">
.profile {
  position: relative;
  z-index: 10;
  display: flex;
  width: 100%;
  min-height: 340px;
  background: var(--white);
  border-top: 1px solid #e8e8e8;

  &__left {
    flex: 1;
    padding: 36px 40px 36px 48px;
    max-width: 58%;
  }

  &__right {
    flex: 0 0 42%;
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  &__name-row {
    display: flex;
    align-items: center;
    gap: 0;          // 括号紧贴；名称展开时自然产生间距
    margin-bottom: 20px;
    overflow: hidden; // 防止展开动画期间溢出
  }

  &__name {
    font-family: var(--font-cn);
    font-size: 36px;
    font-weight: 900;
    letter-spacing: 6px;
    color: var(--dark);
    margin: 0;
    line-height: 1.2;
    display: inline-block; // 宽度可动画化所必需
    overflow: hidden;
    white-space: nowrap;
  }

  &__desc {
    font-family: var(--font-cn);
    font-size: 13.5px;
    line-height: 1.85;
    color: var(--text-body);

    p { margin-bottom: 8px; }
  }

  &__desc-sub {
    font-size: 13px;
    color: var(--text-body);
  }

  &__desc-note {
    font-size: 11px;
    color: var(--gray-mid);
    margin-top: 4px;
  }
}

.berry-accent {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  // mask 将通过 JS 设置，固定尺寸确保 conic-gradient 效果整齐
  width: 28px;
  height: 28px;
  border-radius: 50%;  // 裁剪为圆形区域，使扫描效果呈圆弧状
  will-change: mask;

  img {
    display: block;
    width: 28px;
    height: 28px;
    object-fit: contain;
    pointer-events: none;
    user-select: none;
  }
}

.bracket {
  font-family: var(--font-en);
  font-weight: 300;
  font-size: 18px;
  color: var(--dark);
  flex-shrink: 0;

  &--lg {
    font-size: 32px;
    font-weight: 200;
  }
}

// ── 标签 ──
.tags {
  display: flex;
  flex-direction: column;
  gap: 8px;
  margin-bottom: 20px;

  &__row {
    display: flex;
    gap: 16px;
    flex-wrap: wrap;
  }
}

.tag-group {
  display: flex;
  align-items: stretch;
  overflow: hidden;
}

.tag-label {
  display: flex;
  align-items: center;
  padding: 5px 14px;
  background: var(--yellow);
  color: var(--dark);
  font-family: var(--font-cn);
  font-size: 13px;
  font-weight: 700;
  letter-spacing: 1px;
  white-space: nowrap;
}

.tag-value {
  display: flex;
  align-items: center;
  padding: 5px 16px;
  background: var(--tag-bg);
  color: var(--white);
  font-family: var(--font-cn);
  font-size: 13px;
  font-weight: 400;
  letter-spacing: 0.5px;
  white-space: nowrap;
}

// ── 青色线条与细节 ──
.teal-line {
  width: 100%;
  height: 2px;
  background: var(--teal);
  margin: 8px 0 20px;
  opacity: 0.8;
}

.dot-sep { margin: 0 2px; }

.highlight-red {
  color: var(--accent-red);
  font-weight: 600;
}

// ── 3D 按钮 ──
.model-placeholder {
  width: 100%;
  height: 100%;
}

.btn-3d {
  position: absolute;
  right: 24px;
  bottom: 50%;
  transform: translateY(50%);
  width: 48px;
  height: 48px;
  border-radius: 50%;
  border: 2px solid #ddd;
  background: var(--white);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
  transition: all 0.25s ease;
  z-index: 20;

  &:hover {
    border-color: var(--yellow);
    box-shadow: 0 4px 16px rgba(255, 214, 0, 0.25);
    transform: translateY(50%) scale(1.05);
  }

  &__icon {
    font-family: var(--font-en);
    font-size: 14px;
    font-weight: 700;
    color: var(--dark);
    letter-spacing: 0.5px;
  }
}

// ── 响应式 ──
@media (max-width: 900px) {
  .profile {
    flex-direction: column;

    &__left {
      max-width: 100%;
      padding: 24px;
    }
    &__right {
      flex: none;
      height: 200px;
    }
  }
}

@media (max-width: 600px) {
  .profile__name { font-size: 26px; }

  .bracket--lg { font-size: 24px; }

  .tags__row {
    flex-direction: column;
    gap: 6px;
  }

  .tag-label,
  .tag-value {
    font-size: 11px;
    padding: 4px 10px;
  }

  .profile__desc { font-size: 12px; }
}
</style>
