<template>
  <header class="resume-header">
    <div class="header-main">
      <div class="avatar-wrapper" v-if="avatar">
        <img :src="avatar" alt="李坤的照片" class="avatar-img" />
      </div>

      <div class="identity-content">
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
    </div>
    
    <div class="decoration-line"></div>
  </header>
</template>

<script setup>
import { Message, Phone, Link } from '@element-plus/icons-vue'
// 3. 修改：新增 avatar 接收照片路径
defineProps(['name', 'title', 'email', 'phone', 'github', 'avatar'])
</script>

<style scoped>
.resume-header { 
  margin-bottom: 35px; 
  text-align: left; 
}

/* 1. 头部主区域：增加响应式切换 */
.header-main {
  display: flex;
  align-items: center; 
  gap: 30px; 
  margin-bottom: 20px;
}

.avatar-wrapper {
  flex-shrink: 0; 
}

.avatar-img {
  width: 120px; 
  height: 120px; 
  border-radius: 50%; 
  object-fit: cover; 
  border: 4px solid #fff; 
  box-shadow: 0 4px 12px rgba(0,0,0,0.1); 
  transition: transform 0.3s;
}

.avatar-img:hover {
  transform: scale(1.05);
}

.identity-content {
  display: flex;
  flex-direction: column;
  gap: 10px;
  /* 关键：防止内部长文字撑破容器 */
  min-width: 0; 
}

.name { 
  font-size: 3rem; 
  font-weight: 800; 
  color: #1a1a1a; 
  margin: 0; 
  letter-spacing: 3px; 
  text-transform: uppercase;
  /* 防止名字过长溢出 */
  word-break: break-all;
}

.title-tag { 
  font-size: 1.1rem; 
  color: #42b983; 
  font-weight: 600; 
  margin: 0;
  background: #eefaf3; 
  padding: 4px 18px; 
  border-radius: 20px;
  display: inline-flex; 
  align-items: center; 
  gap: 8px;
}

.dot { width: 6px; height: 6px; background: #42b983; border-radius: 50%; display: inline-block; }

.contact-bar { 
  display: flex; 
  justify-content: flex-start; 
  gap: 20px; 
  flex-wrap: wrap; 
}

.contact-item { 
  display: flex; 
  align-items: center; 
  gap: 8px; 
  font-size: 0.95rem; 
  color: #555;
  /* 强制长邮箱/链接换行 */
  word-break: break-all;
}

.icon-svg { font-size: 1.1rem; color: #888; transition: color 0.2s; }
.contact-item:hover .icon-svg { color: #42b983; }

.contact-item a { 
  color: #555; 
  text-decoration: none; 
  border-bottom: 1px solid transparent; 
  transition: all 0.2s; 
}

.contact-item a:hover { color: #42b983; border-bottom: 1px solid #42b983; }

.decoration-line { 
  margin-top: 10px; 
  height: 3px; 
  background: linear-gradient(90deg, #42b983 0%, #42b983 50%, transparent 100%); 
  opacity: 0.6; 
}

/* --- 2. 手机端专项适配 (核心改动) --- */
@media (max-width: 768px) {
  .resume-header {
    text-align: center; /* 手机端文字居中 */
  }

  .header-main {
    flex-direction: column; /* 头像和名字改为上下排列 */
    gap: 15px;
    margin-bottom: 15px;
  }

  .avatar-img {
    width: 100px; /* 手机端稍微缩小头像 */
    height: 100px;
  }

  .name {
    font-size: 1.8rem; /* 名字字号大幅减小，防止超标 */
    letter-spacing: 1px;
  }

  .title-tag {
    font-size: 0.9rem;
    padding: 3px 12px;
    justify-content: center;
  }

  .contact-bar {
    justify-content: center; /* 联系方式居中显示 */
    gap: 12px;
  }

  .contact-item {
    font-size: 0.85rem; /* 缩小联系方式字体 */
  }

  .decoration-line {
    background: linear-gradient(90deg, transparent 0%, #42b983 50%, transparent 100%);
  }
}

/* 3. 打印调整 */
@media print {
  .avatar-img {
    -webkit-print-color-adjust: exact;
    border: 3px solid #eee;
  }
}
</style>