<script setup lang="ts">
// Kina SaQina — Main Page Composition
// Composes: HeroSection + ProfileSection + PageFooter
import HeroSection from './HeroSection.vue'
import ProfileSection from './ProfileSection.vue'
import PageFooter from './PageFooter.vue'
</script>

<template>
  <div class="page">
    <HeroSection />
    <ProfileSection />
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
