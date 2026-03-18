<template>
  <div class="app-container">
    <div class="toolbar">
      <button class="print-btn" @click="handlePrint">✨ 保存为 PDF</button>
    </div>

    <div class="resume-paper">
      <ResumeHeader v-bind="user" github="github.com/likun-tech" />

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
        "主导后端架构设计，利用 JPA 实现多对多复杂关联查询。",
        "设计并实现基于 Interceptor 的登录验证与后台资源保护机制。",
        "解决实体类级联操作导致的循环序列化问题，优化部署兼容性。"
      ]
    },
    {
      name: "基于 TCP/UDP 的即时通讯系统",
      techStack: "C/Java, Socket, Wireshark",
      details: [
        "基于 TCP 实现大文件分块传输与断点续传，确保数据可靠性。",
        "利用 UDP 配合多线程技术实现高并发消息广播模拟。",
        "通过 Wireshark 抓包分析握手流程，根据拥塞情况优化缓冲区。"
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
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap');

body { 
  background-color: #f4f6f8; margin: 0; padding: 0; 
  font-family: 'Inter', "PingFang SC", "Microsoft YaHei", sans-serif;
  -webkit-font-smoothing: antialiased;
}

.app-container { padding: 50px 0; display: flex; flex-direction: column; align-items: center; }
.toolbar { width: 210mm; display: flex; justify-content: flex-end; margin-bottom: 25px; }
.print-btn { 
  padding: 10px 30px; background: #fff; color: #42b983; border: 1px solid #42b983; 
  border-radius: 30px; cursor: pointer; font-weight: 600; transition: all 0.3s;
}
.print-btn:hover { background: #42b983; color: white; transform: translateY(-1px); }

.resume-paper {
  width: 210mm; min-height: 297mm; background: white;
  padding: 30mm 20mm; box-sizing: border-box; 
  box-shadow: 0 10px 40px rgba(0,0,0,0.06); border-radius: 4px;
}

.edu-grid { display: flex; justify-content: space-between; align-items: baseline; margin-bottom: 12px; }
.edu-main-info { display: flex; gap: 20px; font-weight: 700; color: #1a1a1a; font-size: 1.1rem; }
.edu-details-box { font-size: 0.95rem; color: #555; line-height: 1.7; background: #fbfcfd; padding: 12px 18px; border-radius: 4px; border: 1px solid #f0f0f0; }
.edu-details-box .label { font-weight: 600; color: #333; }

.skills-flex-container { display: flex; flex-direction: column; gap: 12px; }
.skill-group-card { background: #fff; border: 1px solid #eaeaea; padding: 12px 15px; border-radius: 6px; }
.category-name { margin: 0 0 8px 0; font-size: 1rem; color: #333; font-weight: 600; }
.skill-tags { display: flex; flex-wrap: wrap; gap: 8px; }
.skill-tag-single { font-size: 0.85rem; color: #4b5563; background: #f3f4f6; padding: 2px 12px; border-radius: 15px; border: 1px solid transparent; }

.summary-flex-box { display: grid; grid-template-columns: repeat(auto-fit, minmax(240px, 1fr)); gap: 15px; }
.summary-item-card { background: #fbfcfd; padding: 15px; border-radius: 6px; border: 1px solid #f0f0f0; transition: all 0.3s; }
.summary-item-card:hover { transform: translateY(-2px); border-color: #42b983; }
.tag-header { display: flex; align-items: center; gap: 8px; margin-bottom: 8px; color: #1a1a1a; }
.summary-dot { width: 6px; height: 6px; background: #42b983; border-radius: 50%; }
.summary-content { margin: 0; font-size: 0.95rem; color: #555; line-height: 1.6; }

@media print {
  body { background: white; }
  .app-container { padding: 0; }
  .toolbar { display: none; }
  .resume-paper { box-shadow: none; margin: 0; padding: 15mm 15mm; width: 100%; border-radius: 0; }
  .summary-item-card:hover { transform: none; }
  .project-item:hover { transform: none; }
}
</style>