<script setup lang="ts">
// Profile Section — Character name, tags, description, 3D model area
</script>

<template>
  <section class="profile" id="profile-section">
    <div class="profile__left">
      <!-- Character Name -->
      <div class="profile__name-row">
        <div class="berry-accent">
          <svg width="28" height="28" viewBox="0 0 28 28" fill="none">
            <circle cx="14" cy="8" r="3.5" fill="#E8456B"/>
            <circle cx="8" cy="14" r="3.5" fill="#E8456B"/>
            <circle cx="20" cy="14" r="3.5" fill="#E8456B"/>
            <circle cx="11" cy="20" r="3.5" fill="#E8456B"/>
            <circle cx="17" cy="20" r="3.5" fill="#E8456B"/>
            <line x1="14" y1="2" x2="14" y2="0" stroke="#4CAF50" stroke-width="2"/>
            <path d="M12 3 Q14 0 16 3" fill="#4CAF50"/>
          </svg>
        </div>
        <span class="bracket bracket--lg">[</span>
        <h1 class="profile__name">绮娜·萨琪娜</h1>
        <span class="bracket bracket--lg">]</span>
      </div>

      <!-- Tags Grid -->
      <div class="tags">
        <div class="tags__row">
          <div class="tag-group">
            <span class="tag-label">阵营</span>
            <span class="tag-value">北理工网协</span>
          </div>
          <div class="tag-group">
            <span class="tag-label">种族</span>
            <span class="tag-value">技术·数据</span>
          </div>
        </div>
        <div class="tags__row">
          <div class="tag-group">
            <span class="tag-label">中文</span>
            <span class="tag-value">来自北方的乐</span>
          </div>
          <div class="tag-group">
            <span class="tag-label">英文</span>
            <span class="tag-value">来自北方的乐</span>
          </div>
        </div>
      </div>

      <!-- Teal Accent Line -->
      <div class="teal-line"></div>

      <!-- Description -->
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

    <!-- Right Side (3D Model Area) -->
    <div class="profile__right">
      <div class="model-placeholder">
        <!-- 3D model area — will be powered by Three.js -->
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
    gap: 10px;
    margin-bottom: 20px;
  }

  &__name {
    font-family: var(--font-cn);
    font-size: 36px;
    font-weight: 900;
    letter-spacing: 6px;
    color: var(--dark);
    margin: 0;
    line-height: 1.2;
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
}

.bracket {
  font-family: var(--font-en);
  font-weight: 300;
  font-size: 18px;
  color: var(--dark);

  &--lg {
    font-size: 32px;
    font-weight: 200;
  }
}

// ── Tags ──
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

// ── Teal Line & Details ──
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

// ── 3D Button ──
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

// ── Responsive ──
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
