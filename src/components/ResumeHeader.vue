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
.resume-header { margin-bottom: 35px; text-align: left; /* 4. 修改：整体改为左对齐 */ }

/* 5. 新增：头部主区域布局 */
.header-main {
  display: flex;
  align-items: center; /* 垂直居中 */
  gap: 30px; /* 照片和文字的间距 */
  margin-bottom: 20px;
}

/* 6. 新增：照片样式 */
.avatar-wrapper {
  flex-shrink: 0; /* 防止照片被压缩 */
}
.avatar-img {
  width: 120px; /* 照片宽度 */
  height: 120px; /* 照片高度，保持正方形 */
  border-radius: 50%; /* 圆形照片 */
  object-fit: cover; /* 确保图片不发生形变 */
  border: 4px solid #fff; /* 白色边框 */
  box-shadow: 0 4px 12px rgba(0,0,0,0.1); /* 细腻的阴影 */
  transition: transform 0.3s;
}
.avatar-img:hover {
  transform: scale(1.05); /* 悬停时微微放大 */
}

/* 7. 新增：身份信息区域布局 */
.identity-content {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.name { 
  font-size: 3rem; font-weight: 800; color: #1a1a1a; margin: 0; 
  letter-spacing: 3px; text-transform: uppercase;
}
.title-tag { 
  font-size: 1.1rem; color: #42b983; font-weight: 600; margin: 0;
  background: #eefaf3; padding: 4px 18px; border-radius: 20px;
  display: inline-flex; align-items: center; gap: 8px;
}
.dot { width: 6px; height: 6px; background: #42b983; border-radius: 50%; display: inline-block; }

/* 8. 修改：联系方式布局 */
.contact-bar { display: flex; justify-content: flex-start; gap: 25px; flex-wrap: wrap; }
.contact-item { display: flex; align-items: center; gap: 8px; font-size: 0.95rem; color: #555; }
.icon-svg { font-size: 1.1rem; color: #888; transition: color 0.2s; }
.contact-item:hover .icon-svg { color: #42b983; }
.contact-item a { color: #555; text-decoration: none; border-bottom: 1px solid transparent; transition: all 0.2s; }
.contact-item a:hover { color: #42b983; border-bottom: 1px solid #42b983; }

.decoration-line { margin-top: 10px; height: 3px; background: linear-gradient(90deg, #42b983 0%, #42b983 50%, transparent 100%); opacity: 0.6; }

/* 9. 新增：打印时的调整 */
@media print {
  .avatar-img {
    -webkit-print-color-adjust: exact; /* 确保打印时保留边框和阴影 */
    border: 3px solid #eee; /* 打印时边框稍微显眼一点 */
  }
}
</style>