<script setup lang="ts">
// 页脚 — 与参考设计匹配的完整页脚
// 区块：顶部导航链接、信息栏、Logo+版权、标准徽章、年龄分级
</script>

<template>
  <footer class="footer" id="footer-section">

    <!-- ── 顶部导航链接 ── -->
    <div class="footer__nav">
      <a href="#" class="footer__nav-link">【网视融媒】Live2D虚拟形象配套许可及配套协议</a>
      <span class="footer__nav-sep">|</span>
      <a href="#" class="footer__nav-link">网络开拓者协会虚拟形象推广政策</a>
      <span class="footer__nav-sep">|</span>
      <a href="#" class="footer__nav-link">网络开拓者协会虚拟形象管理政策</a>
      <span class="footer__nav-sep">|</span>
      <a href="#" class="footer__nav-link">云端指南与开源协议</a>
    </div>

    <!-- ── 信息栏 ── -->
    <div class="footer__info">
      <div class="footer__info-col">
        <p class="footer__info-line">北京市1702区4号楼1</p>
        <p class="footer__info-line">全国网络标识 241014030101@网络</p>
      </div>
      <div class="footer__info-col">
        <p class="footer__info-line">官网电话：[2024] 0413-9402号</p>
      </div>
      <div class="footer__info-col">
        <p class="footer__info-line">官网注册：[2014] 1755号</p>
      </div>
      <div class="footer__info-col">
        <p class="footer__info-line">IEB: 079-7-4X5-13884-2</p>
      </div>
    </div>

    <!-- ── 分隔线（一）── -->
    <div class="footer__divider"></div>

    <!-- ── 免责声明文字 ── -->
    <div class="footer__disclaimer">
      <p>
        声明/免责说明：「网站」是「网络开拓者协会」时间网不同个人、组织、单位合法公议计约书所盟"空闻组织"支持下打造圈内信息重镇
        在官订号"形象猫"赛事圆满组织已提认识。赛去网站：www.bitneonrising.com 参赛报名 联系电话：114 3113191&
      </p>
    </div>

    <!-- ── 分隔线（二）── -->
    <div class="footer__divider"></div>

    <!-- ── Logo + 版权行 ── -->
    <div class="footer__brand-row">
      <!-- Logo 区块 -->
      <div class="footer__logo-block">
        <img src="/kina/takina_hero.png" alt="Inoue Takina" class="footer__logo-img" />
        <div class="footer__logo-text">
          <span class="footer__logo-name">井ノ上 瀧奈</span>
          <span class="footer__logo-sub">INOUE<br>TAKINA</span>
        </div>
      </div>

      <!-- 版权 + 联系方式 -->
      <div class="footer__copyright-block">
        <p class="footer__open">开放台：网络开拓者协会虚拟社运联网联联联</p>
        <p class="footer__copy">Copyright©2023-2026 网络开拓者协会虚拟技术协四技术协议所属版权 官服电话：114-314-2919</p>
        <div class="footer__standards-row">
          <span class="footer__std-label">全企业标准违法及犯罪举报中心</span>
          <span class="footer__std-sep">|</span>
          <span class="footer__std-label">北京高等院校违法及犯罪中心举报</span>
        </div>
      </div>
    </div>

    <!-- ── 底部分隔线 ── -->
    <div class="footer__divider"></div>

    <!-- ── 标准徽章与年龄分级行 ── -->
    <div class="footer__bottom-row">
      <!-- 年龄分级徽章 -->
      <div class="footer__age-badge">
        <div class="footer__age-icon">
          <span class="footer__age-num">12+</span>
          <span class="footer__age-label">适龄提示</span>
        </div>
        <div class="footer__age-text">
          <p>该游戏未获"游戏许可证"即在本平台处供18岁以上用户，为了您的身心健康，请合理游戏不长大游！</p>
          <p>根据相关法规规定，网络游戏用户需实名注册，未成年用户应在监护人监护，指导下使用本产品，注意维护网络安全，</p>
          <p>勿沉迷网游戏，合理安排游戏时间，适度游戏有益身心 切勿沉迷游戏荣耀！</p>
        </div>
      </div>

      <!-- 标准标签 -->
      <div class="footer__std-badges">
        <img src="/standar/cadpa.png" alt="CADPA 标准" class="footer__std-img" />
        <img src="/standar/igrs.png" alt="IGRS 标准" class="footer__std-img" />
      </div>
    </div>

    <!-- ── 向下滚动箭头 ── -->
    <div class="footer__scroll-arrow">
      <svg width="32" height="18" viewBox="0 0 32 18" fill="none">
        <polyline points="4,4 16,14 28,4" stroke="#FFD600" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"/>
      </svg>
    </div>

  </footer>
</template>

<style scoped lang="scss">
.footer {
  width: 100%;
  background: #0d0d0d;
  color: rgba(255, 255, 255, 0.65);
  font-family: var(--font-cn);
  padding: 28px 48px 16px;
  display: flex;
  flex-direction: column;
  gap: 0;

  // ── 顶部导航链接 ──
  &__nav {
    display: flex;
    align-items: center;
    flex-wrap: wrap;
    gap: 6px 0;
    margin-bottom: 16px;
  }

  &__nav-link {
    font-size: 11px;
    color: rgba(255, 255, 255, 0.7);
    text-decoration: none;
    letter-spacing: 0.3px;
    transition: color 0.2s;

    &:hover { color: var(--yellow); }
  }

  &__nav-sep {
    margin: 0 10px;
    color: rgba(255, 255, 255, 0.25);
    font-size: 11px;
  }

  // ── 分隔线 ──
  &__divider {
    width: 100%;
    height: 1px;
    background: rgba(255, 255, 255, 0.1);
    margin: 12px 0;
  }

  // ── 信息栏 ──
  &__info {
    display: flex;
    flex-wrap: wrap;
    gap: 8px 40px;
    margin-bottom: 4px;
  }

  &__info-col {
    display: flex;
    flex-direction: column;
    gap: 2px;
  }

  &__info-line {
    font-size: 11px;
    color: rgba(255, 255, 255, 0.55);
    margin: 0;
    line-height: 1.6;
  }

  // ── 免责声明 ──
  &__disclaimer {
    font-size: 11px;
    color: rgba(255, 255, 255, 0.45);
    line-height: 1.7;
    margin: 4px 0;

    p { margin: 0; }
  }

  // ── 品牌行 ──
  &__brand-row {
    display: flex;
    align-items: flex-start;
    gap: 32px;
    padding: 8px 0;
  }

  &__logo-block {
    display: flex;
    align-items: center;
    gap: 10px;
    flex-shrink: 0;
  }

  &__logo-img {
    width: 64px;
    height: 64px;
    object-fit: contain;
    border-radius: 4px;
    filter: brightness(0.9);
  }

  &__logo-text {
    display: flex;
    flex-direction: column;
    gap: 0;
  }

  &__logo-name {
    font-family: var(--font-cn);
    font-size: 22px;
    font-weight: 700;
    color: rgba(255, 255, 255, 0.85);
    letter-spacing: 2px;
    line-height: 1.2;
  }

  &__logo-sub {
    font-family: var(--font-en);
    font-size: 10px;
    font-weight: 800;
    color: var(--yellow);
    letter-spacing: 3px;
    line-height: 1.3;
    text-transform: uppercase;
  }

  &__copyright-block {
    display: flex;
    flex-direction: column;
    gap: 4px;
    flex: 1;
  }

  &__open {
    font-size: 11px;
    color: rgba(255, 255, 255, 0.55);
    margin: 0;
  }

  &__copy {
    font-size: 11px;
    color: rgba(255, 255, 255, 0.45);
    margin: 0;
    line-height: 1.6;
  }

  &__standards-row {
    display: flex;
    align-items: center;
    gap: 0;
    margin-top: 4px;
  }

  &__std-label {
    font-size: 11px;
    color: rgba(255, 255, 255, 0.5);
  }

  &__std-sep {
    margin: 0 10px;
    color: rgba(255, 255, 255, 0.2);
    font-size: 11px;
  }

  // ── 底部行 ──
  &__bottom-row {
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
    gap: 24px;
    padding: 8px 0 4px;
    flex-wrap: wrap;
  }

  // ── 年龄分级徽章 ──
  &__age-badge {
    display: flex;
    align-items: flex-start;
    gap: 14px;
    flex: 1;
    min-width: 260px;
  }

  &__age-icon {
    flex-shrink: 0;
    width: 56px;
    height: 60px;
    border: 2px solid var(--yellow);
    border-radius: 6px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background: rgba(255, 214, 0, 0.06);
  }

  &__age-num {
    font-family: var(--font-en);
    font-size: 20px;
    font-weight: 900;
    color: var(--yellow);
    line-height: 1;
  }

  &__age-label {
    font-size: 9px;
    color: var(--yellow);
    letter-spacing: 1px;
    margin-top: 2px;
  }

  &__age-text {
    flex: 1;

    p {
      font-size: 10px;
      color: rgba(255, 255, 255, 0.4);
      margin: 0 0 2px;
      line-height: 1.6;
    }
  }

  // ── 标准徽章 ──
  &__std-badges {
    display: flex;
    align-items: center;
    gap: 12px;
    flex-shrink: 0;
    align-self: center;
  }

  &__std-img {
    height: 44px;
    width: auto;
    object-fit: contain;
    filter: brightness(0.85) grayscale(0.1);
  }

  // ── 向下滚动箭头 ──
  &__scroll-arrow {
    display: flex;
    justify-content: center;
    padding: 12px 0 4px;
    opacity: 0.5;
  }
}

// ── 响应式 ──
@media (max-width: 900px) {
  .footer {
    padding: 20px 24px 12px;

    &__info { gap: 6px 20px; }
    &__brand-row { flex-direction: column; gap: 16px; }
    &__bottom-row { flex-direction: column; }
    &__std-badges { align-self: flex-start; }
  }
}

@media (max-width: 600px) {
  .footer {
    padding: 16px 16px 10px;

    &__nav { gap: 4px 0; }
    &__nav-link { font-size: 10px; }
    &__logo-img { width: 48px; height: 48px; }
    &__logo-name { font-size: 18px; }
  }
}
</style>
