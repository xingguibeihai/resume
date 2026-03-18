<template>
  <div class="app-container">
    <div class="toolbar">
      <button class="print-btn" @click="handlePrint">✨ 保存为 PDF</button>
    </div>

    <div class="resume-paper">
      <ResumeHeader 
        v-bind="user" 
        :avatar="avatarUrl"
        github="github.com/xingguibeihai" 
      />

      <main>
        <ResumeSection title="教育背景">
          <div class="edu-grid">
            <div class="edu-main-info">
              <span class="school">{{ user.education.school }}</span>
              <span class="major">{{ user.education.major }}</span>
            </div>
            <span class="date">{{ user.education.date }}</span>
          </div>
          <div class="edu-details-box">
            <p><span class="label">核心课程：</span>{{ user.education.courses.join('、') }}</p>
            <p><span class="label">实践项目：</span>{{ user.education.practice }}</p>
          </div>
        </ResumeSection>

        <ResumeSection title="项目经历">
          <div class="project-wrapper">
            <ProjectItem v-for="proj in user.projects" :key="proj.name" v-bind="proj" />
          </div>
        </ResumeSection>

        <ResumeSection title="专业技能">
          <div class="skills-flex-container">
            <div v-for="(list, category) in user.skills" :key="category" class="skill-group-card">
              <h4 class="category-name">{{ category }}</h4>
              <div class="skill-tags">
                <span v-for="skill in list" :key="skill" class="skill-tag-single">{{ skill }}</span>
              </div>
            </div>
          </div>
        </ResumeSection>

        <ResumeSection title="个人优势">
          <div class="summary-flex-box">
            <div v-for="item in user.summary" :key="item.tag" class="summary-item-card">
              <div class="tag-header">
                <span class="summary-dot"></span>
                <strong>{{ item.tag }}</strong>
              </div>
              <p class="summary-content">{{ item.content }}</p>
            </div>
          </div>
        </ResumeSection>
      </main>
    </div>
  </div>
</template>

<script setup>
import { reactive } from 'vue'
import ResumeHeader from './components/ResumeHeader.vue'
import ResumeSection from './components/ResumeSection.vue'
import ProjectItem from './components/ProjectItem.vue'

// 1. 新增：导入照片文件
// 请确保在 src/assets/ 下有 avatar.jpg 文件
import avatarUrl from './assets/avatar.jpg'

const handlePrint = () => window.print()

const user = reactive({
  name: "李坤",
  title: "网络工程专业 | 全栈开发方向",
  email: "2978131465@qq.com",
  phone: "134-0847-3433",
  education: {
    school: "成都信息工程大学",
    major: "网络工程",
    date: "2023 - 2027",
    courses: ["计算机网络", "TCP/IP 协议", "路由与交换技术", "操作系统", "数据库系统"],
    practice: "基于单臂路由与 OSPF 的校园网设计"
  },
  projects: [
    {
      name: "MyBlog 全栈博客管理系统",
      techStack: "Spring Boot, JPA, MySQL, Vue",
      details: [
        "技术栈： Spring Boot, Spring Data JPA, MySQL, Thymeleaf/Vue, Maven",
        "核心内容：主导后端架构设计，利用 JPA 结合 MySQL 实现文章、分类、标签的多对多复杂关联查询。针对用户权限，设计并实现基于 Interceptor（拦截器） 的登录验证与后台资源保护机制。",
        "难点攻克： 解决了实体类级联操作导致的循环序列化问题，并优化了数据库方言配置以提升部署兼容性。"
      ]
    },
    {
      name: "基于 TCP/UDP 的即时通讯系统",
      techStack: "C/Java, Socket, Wireshark",
      details: [
        "技术栈： C/Java, Socket API, 多线程, IO 流, Wireshark",
        "核心内容：文件传输： 基于 TCP 协议实现大文件分块传输与断点续传思路，确保数据传输的完整性与可靠性。即时通讯： 利用 UDP 协议配合多线程技术实现高并发消息广播，模拟多客户端在线交互场景。协议分析： 使用 Wireshark 抓包分析三次握手与四次挥手过程，根据网络拥塞情况调整缓冲区大小，优化传输效率。"
      ]
    },
    {
      name: "第二课堂管理系统 (数据库专项)",
      techStack: "SQL, E-R 模型, 事务控制",
      details: [
        "完成 10 余张核心业务表的 E-R 模型设计，应用三范式标准优化结构。",
        "编写复杂 SQL 统计语句实现学分汇总，利用事务确保数据原子性。"
      ]
    }
  ],
  skills: {
    "编程语言": ["Java (熟练)", "C/C++ (基础)", "SQL", "HTML/JavaScript"],
    "后端开发": ["Spring Boot", "Spring Data JPA", "Hibernate", "Maven"],
    "数据库": ["MySQL (索引优化、事务管理、复杂查询)"],
    "网络/工具": ["Cisco Packet Tracer", "Wireshark", "Linux", "Git"]
  },
  summary: [
    { tag: "网络基础", content: "精通 TCP/IP 协议栈，熟悉 OSPF、RIP 等路由协议及 VLAN/NAT 配置。" },
    { tag: "全栈能力", content: "熟练掌握 Java 生态（Spring Boot/JPA），具备 MySQL 建模与优化经验。" },
    { tag: "底层调试", content: "能使用 Wireshark 进行协议分析，具备 C 语言底层开发基础。" }
  ]
})
</script>

<style>
/* 1. 全局重置：确保所有元素的边距计算包含在宽度内，防止撑破边框 */
* {
  box-sizing: border-box;
}

@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap');

body { 
  background-color: #f4f6f8; 
  margin: 0; 
  padding: 0; 
  font-family: 'Inter', "PingFang SC", "Microsoft YaHei", sans-serif;
  -webkit-font-smoothing: antialiased;
  /* 防止移动端横向滑动 */
  overflow-x: hidden; 
}

/* 2. 外部容器：居中且防溢出 */
.app-container { 
  width: 100%;
  display: flex; 
  flex-direction: column; 
  align-items: center; 
  padding: 20px 10px; 
}

.toolbar { 
  width: 100%;
  max-width: 210mm; 
  display: flex; 
  justify-content: flex-end; 
  margin-bottom: 20px; 
}

.print-btn { 
  padding: 8px 20px; background: #fff; color: #42b983; border: 1px solid #42b983; 
  border-radius: 30px; cursor: pointer; font-weight: 600; transition: all 0.3s;
}

/* 3. 简历纸张：宽度自适应核心 */
.resume-paper {
  width: 100%;           /* 默认占满全屏 */
  max-width: 210mm;      /* 电脑端限制为 A4 宽度 */
  background: white;
  padding: 15mm;         /* 初始边距 */
  box-shadow: 0 10px 40px rgba(0,0,0,0.06); 
  border-radius: 4px;
  /* 关键：防止长文本（邮箱/代码）撑开容器 */
  word-wrap: break-word;
  word-break: break-word; 
  overflow-wrap: break-word;
}

/* 4. 排版组件：确保 Flex 布局能自动换行 */
.edu-grid { 
  display: flex; 
  justify-content: space-between; 
  align-items: baseline; 
  margin-bottom: 12px; 
  gap: 10px;
}

.edu-main-info { 
  display: flex; 
  gap: 15px; 
  font-weight: 700; 
  color: #1a1a1a; 
  font-size: 1.1rem; 
  flex-wrap: wrap; /* 允许学校和专业在窄屏时换行 */
}

.edu-details-box { 
  font-size: 0.95rem; 
  color: #555; 
  line-height: 1.6; 
  background: #fbfcfd; 
  padding: 12px; 
  border-radius: 4px; 
  border: 1px solid #f0f0f0; 
}

.skills-flex-container { display: flex; flex-direction: column; gap: 10px; }
.skill-group-card { background: #fff; border: 1px solid #eaeaea; padding: 10px; border-radius: 6px; }
.skill-tags { display: flex; flex-wrap: wrap; gap: 6px; }
.skill-tag-single { font-size: 0.85rem; padding: 2px 10px; background: #f3f4f6; border-radius: 12px; }

/* 5. 总结区域：使用响应式网格 */
.summary-flex-box { 
  display: grid; 
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); 
  gap: 15px; 
}

/* 6. --- 移动端专项极限适配 (针对手机屏幕) --- */
@media (max-width: 768px) {
  .app-container { padding: 10px 5px; }
  
  .resume-paper { 
    padding: 20px 15px; /* 进一步缩小内边距 */
    border-radius: 0;    /* 手机端取消圆角，利用空间 */
  }

  /* 缩小字体大小，防止标题溢出 */
  h1 { font-size: 1.8rem !important; } 
  .edu-main-info { font-size: 0.95rem; }
  
  .edu-grid { 
    flex-direction: column; 
    align-items: flex-start; 
  }

  /* 强制所有卡片在手机端单列显示 */
  .summary-flex-box { 
    grid-template-columns: 1fr; 
  }

  /* 关键：联系方式等长字符串在窄屏下强制换行 */
  a, span, p {
    overflow-wrap: break-word;
    word-wrap: break-word;
    word-break: break-all;
  }
}

/* 7. 打印控制 */
@media print {
  body { background: white; }
  .app-container { padding: 0; }
  .toolbar { display: none; }
  .resume-paper { 
    box-shadow: none; 
    margin: 0; 
    padding: 15mm; 
    width: 210mm; 
    border-radius: 0; 
  }
}
</style>