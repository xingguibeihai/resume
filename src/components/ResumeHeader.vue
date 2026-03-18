<template>
  <header class="resume-header">
    <div class="header-content">
      <div class="identity">
        <h1 class="name">{{ name }}</h1>
        <p class="title-tag">
          <span class="dot"></span>
          {{ title }}
        </p>
      </div>

      <div class="contact-bar">
        <div class="contact-item">
          <el-icon class="icon-svg"><Message /></el-icon>
          <a :href="'mailto:' + email">{{ email }}</a>
        </div>
        <div class="contact-item">
          <el-icon class="icon-svg"><Phone /></el-icon>
          <span>{{ phone }}</span>
        </div>
        <div class="contact-item" v-if="github">
          <el-icon class="icon-svg"><Link /></el-icon>
          <a :href="'https://' + github" target="_blank">GitHub</a>
        </div>
      </div>
    </div>
    <div class="decoration-line"></div>
  </header>
</template>

<script setup>
import { Message, Phone, Link } from '@element-plus/icons-vue'
defineProps(['name', 'title', 'email', 'phone', 'github'])
</script>

<style scoped>
.resume-header { margin-bottom: 35px; text-align: center; }
.name { font-size: 3rem; font-weight: 800; color: #1a1a1a; margin: 0; letter-spacing: 3px; }
.title-tag { 
  font-size: 1.1rem; color: #42b983; font-weight: 600; margin: 10px 0;
  background: #eefaf3; padding: 4px 18px; border-radius: 20px;
  display: inline-flex; align-items: center; gap: 8px;
}
.dot { width: 6px; height: 6px; background: #42b983; border-radius: 50%; display: inline-block; }
.contact-bar { display: flex; justify-content: center; gap: 30px; margin-top: 20px; flex-wrap: wrap; }
.contact-item { display: flex; align-items: center; gap: 8px; font-size: 1rem; color: #555; }
.icon-svg { font-size: 1.1rem; color: #888; transition: color 0.2s; }
.contact-item:hover .icon-svg { color: #42b983; }
.contact-item a { color: #555; text-decoration: none; border-bottom: 1px solid transparent; transition: all 0.2s; }
.contact-item a:hover { color: #42b983; border-bottom: 1px solid #42b983; }
.decoration-line { margin-top: 30px; height: 3px; background: linear-gradient(90deg, transparent, #42b983 50%, transparent); opacity: 0.6; }
</style>