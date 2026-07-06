<script setup lang="ts">
// Inoue Takina — 页面主体组合
// 组成：英雄区 + 资料区 + 详情区 + 页脚
import HeroSection from './HeroSection.vue'
import ProfileSection from './ProfileSection.vue'
import DetailSection from './DetailSection.vue'
import PageFooter from './PageFooter.vue'
</script>

<template>
  <div class="page">
    <HeroSection />
    <ProfileSection />
    <DetailSection />
    <PageFooter />
  </div>
</template>

<style scoped lang="scss">
.page {
  position: relative;
  width: 100%;
  min-height: 100vh;
  overflow: hidden;
  background: var(--white);
}
</style>
