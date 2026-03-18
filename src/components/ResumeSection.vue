<template>
  <section class="resume-section">
    <div class="section-title-wrapper">
      <h2 class="section-title">{{ title }}</h2>
      <div class="title-deco-line"></div>
    </div>
    <div class="section-content">
      <slot />
    </div>
  </section>
</template>

<script setup>
defineProps(['title'])
</script>

<style scoped>
.resume-section { margin-bottom: 30px; }
.section-title-wrapper { display: flex; align-items: center; gap: 15px; margin-bottom: 20px; }
.section-title { font-size: 1.3rem; color: #2c3e50; font-weight: 700; margin: 0; letter-spacing: 1px; }
.title-deco-line { flex-grow: 1; height: 2px; background: #eaeaea; position: relative; }
.title-deco-line::before { content: ''; position: absolute; left: 0; top: 0; width: 40px; height: 100%; background: #42b983; }
.section-content { padding-left: 10px; }
</style>