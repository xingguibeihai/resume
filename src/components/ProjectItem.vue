<template>
  <div class="project-item">
    <div class="project-header">
      <h3 class="name">{{ name }}</h3>
      <span class="tech-tag">{{ techStack }}</span>
    </div>
    <ul class="star-list">
      <li v-for="(detail, index) in details" :key="index">{{ detail }}</li>
    </ul>
  </div>
</template>

<script setup>
defineProps(['name', 'techStack', 'details'])
</script>

<style scoped>
.project-item { padding: 15px; border-radius: 6px; transition: all 0.3s; border: 1px solid transparent; margin-bottom: 10px; }
.project-item:hover { background: #fbfcfd; border-color: #f0f0f0; transform: translateX(4px); }
.project-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px; }
.name { font-size: 1.15rem; color: #1a1a1a; margin: 0; font-weight: 700; }
.tech-tag { font-size: 0.8rem; color: #42b983; background: #f0fdf4; padding: 2px 10px; border-radius: 4px; border: 1px solid #bbf7d0; font-weight: 500; }
.star-list { padding-left: 20px; margin: 0; color: #4b5563; font-size: 0.95rem; line-height: 1.8; }
.star-list li { margin-bottom: 4px; position: relative; }
</style>