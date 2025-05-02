<template>
  <el-container style="height: 500px; border: 1px solid #eee">
    <el-header class="head">
      <div class="header-content">
        <!-- 左侧Logo -->
        <div class="logo-container">
          
        </div>
        <!-- 右侧导航按钮 -->
        <div class="nav-buttons">
          <div 
            v-for="role in roles"
            :key="role.value"
            class="nav-button"
            :class="{ 
              'active': store.role === role.value,
              'inactive': store.role && store.role !== role.value
            }"
            @click="switchRole(role.value)"
          >
            {{ role.label }}
          </div>
        </div>
      </div>
    </el-header>

    <el-container class="main-container">
      <!-- 背景图片层 -->
      <div class="background-layer"></div>

      <!-- 内容层 -->
      <div class="content-layer">
        <el-row class="h-screen"> 
          <el-col :span="24" class="p-8">
            <transition name="fade" mode="out-in">
              <!-- 学生功能 -->
              <el-row 
                v-if="store.role === 'student'" 
                :gutter="40" 
                type="flex"
                justify="center"
                align="middle"
                class="min-h-[70vh]"
              >
                <el-col 
                  v-for="item in studentLinks" 
                  :key="item.path"
                  :xs="24" 
                  :sm="12" 
                  :md="8"
                  :lg="6"
                  class="mb-8 flex justify-center"
                >
                  <el-card 
                    shadow="hover" 
                    class="feature-card cursor-pointer w-full max-w-[320px]"
                    @click="$router.push(item.path)"
                  >
                    <div class="flex flex-col items-center p-6">
                      <el-icon class="text-4xl mb-4 text-blue-500">
                        <component :is="item.icon" />
                      </el-icon>
                      <h3 class="text-lg font-medium mb-2">{{ item.label }}</h3>
                      <p class="text-gray-600 text-center text-sm">{{ item.description }}</p>
                    </div>
                  </el-card>
                </el-col>
              </el-row>

              <!-- 教师功能 -->
              <el-row 
                v-else-if="store.role === 'teacher'"
                :gutter="40"
                type="flex"
                justify="center"
                align="middle"
                class="min-h-[70vh]"
              >
                <el-col 
                  v-for="item in teacherLinks" 
                  :key="item.path"
                  :xs="24" 
                  :sm="12" 
                  :md="8"
                  :lg="6"
                  class="mb-8 flex justify-center"
                >
                  <el-card 
                    shadow="hover" 
                    class="feature-card cursor-pointer w-full max-w-[320px]"
                    @click="$router.push(item.path)"
                  >
                    <div class="flex flex-col items-center p-6">
                      <el-icon class="text-4xl mb-4 text-green-500">
                        <component :is="item.icon" />
                      </el-icon>
                      <h3 class="text-lg font-medium mb-2">{{ item.label }}</h3>
                      <p class="text-gray-600 text-center text-sm">{{ item.description }}</p>
                    </div>
                  </el-card>
                </el-col>
              </el-row>

              <!-- 企业 -->
              <el-row 
                v-else-if="store.role === 'company'"
                :gutter="40"
                type="flex"
                justify="center"
                align="middle"
                class="min-h-[70vh]"
              >
                <!-- 内容结构同上 -->
              </el-row>

              <!-- 社区 -->
              <el-row 
                v-else-if="store.role === 'community'"
                :gutter="40"
                type="flex"
                justify="center"
                align="middle"
                class="min-h-[70vh]"
              >
                <!-- 内容结构同上 -->
              </el-row>

              <!-- 个人中心 -->
              <el-row 
                v-else-if="store.role === 'profile'"
                :gutter="40"
                type="flex"
                justify="center"
                align="middle"
                class="min-h-[70vh]"
              >
                <!-- 内容结构同上 -->
              </el-row>
            </transition>
          </el-col>
        </el-row>
      </div>
    </el-container>
  </el-container>
</template>

<script setup>
import { useUserStore } from '../store'
import { storeToRefs } from 'pinia'

const store = useUserStore()
const { role } = storeToRefs(store)

const switchRole = (selectedRole) => {
  store.role = selectedRole
}

const roles = [
  { value: 'student', label: '学生' },
  { value: 'teacher', label: '教师' },
  { value: 'company', label: '企业' },
  { value: 'community', label: '社区' },
  { value: 'profile', label: '个人中心' }
]

const studentLinks = [
  { 
    path: '/student-plan', 
    label: '学习计划', 
    icon: 'Notebook',
    description: '规划您的学习路径，追踪进度和目标'
  },
  { 
    path: '/code-ide', 
    label: '代码练习', 
    icon: 'Edit',
    description: '在线编写和测试代码，提升编程技能'
  },
  { 
    path: '/interview', 
    label: '模拟面试', 
    icon: 'ChatLineRound',
    description: '准备技术面试，增强求职竞争力'
  }
]

const teacherLinks = [
  { 
    path: '/teaching', 
    label: '课程管理', 
    icon: 'Reading',
    description: '创建和管理您的教学课程内容'
  },
  { 
    path: '/students', 
    label: '学生管理', 
    icon: 'User',
    description: '查看和管理学生名单与学习情况'
  },
  { 
    path: '/assignments', 
    label: '作业批改', 
    icon: 'Collection',
    description: '审阅和评分学生提交的作业'
  }
]

const companyLinks = [
  { 
    path: '/risk', 
    label: '风险控制', 
    icon: 'Warning',
    description: '监控和管理企业运营中的潜在风险'
  },
  { 
    path: '/talents', 
    label: '人才招聘', 
    icon: 'UserFilled',
    description: '发布职位并筛选合适的技术人才'
  },
  { 
    path: '/analytics', 
    label: '数据分析', 
    icon: 'DataAnalysis',
    description: '查看关键业务指标和分析报告'
  }
]

const communityLinks = [
  { 
    path: '/community', 
    label: '进入社区', 
    icon: 'ChatDotRound',
    description: '加入开发者社区，分享知识和经验'
  },
  { 
    path: '/forum', 
    label: '技术论坛', 
    icon: 'ChatLineRound',
    description: '参与技术讨论，解决问题和分享见解'
  },
  { 
    path: '/events', 
    label: '社区活动', 
    icon: 'Bell',
    description: '查看和参与线上线下技术活动'
  }
]

const profileLinks = [
  { 
    path: '/profile', 
    label: '查看个人信息', 
    icon: 'Postcard',
    description: '管理您的个人资料和账户信息'
  },
  { 
    path: '/settings', 
    label: '账号设置', 
    icon: 'Setting',
    description: '调整您的偏好和安全设置'
  },
  { 
    path: '/achievements', 
    label: '我的成就', 
    icon: 'Trophy',
    description: '查看您获得的技能徽章和认证'
  }
]
</script>

<style scoped>
.header-container {
  padding: 0 80px; /* 两侧留白 */
  height: 64px;
  border-bottom: 1px solid #ebeef5;
  height: 70px;  /* 增加高度适应大字体 */

  /* 底部阴影分割线 */
  &::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    height: 1px;
    background: linear-gradient(
      90deg, 
      rgba(228, 231, 237, 0) 0%, 
      rgba(228, 231, 237, 1) 50%, 
      rgba(228, 231, 237, 0) 100%
    );
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.05);
  }
}

.header-content {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 100%;
  max-width: 1440px;
  margin: 0 auto;
  border-bottom: 1px solid #e4e7ed;  /* 新增实体分割线 */
}

.logo-container {
  width: 160px;
}

.logo {
  height: 40px;
}

.nav-buttons {
  display: flex;
  gap: 32px; /* 按钮间距 */
}

.nav-button {
  position: relative;
  padding: 8px 16px;
  font-size: 16px;  /* 从15px调整为16px */
  font-weight: 500;  /* 中等字重 */
  color: #606266;
  cursor: pointer;
  transition: all 0.3s ease;

  /* 默认状态 */
  &::after {
    content: '';
    position: absolute;
    bottom: -4px;
    left: 50%;
    width: 0;
    height: 2px;
    background: transparent;
    transition: all 0.3s ease;
  }

  /* 悬停状态 */
  &:hover {
    color: #409eff;
    transform: translateY(-1px);
    &::after {
      width: 100%;
      left: 0;
      background: #409eff;
    }
  }

  /* 激活状态 */
  &.active {
    color: #409eff;
    font-weight: 500;
    font-size: 17px;  /* 激活状态略微放大 */

    &::after {
      width: 100%;
      left: 0;
      background: #409eff;
      height: 3px;  /* 加粗下划线 */
      bottom: -6px;
    }
  }

  /* 非激活状态 */
  &.inactive {
    opacity: 0.6;
    &:hover {
      opacity: 1;
    }
  }
}

/* 容器样式 */
.main-container {
  padding: 0 80px; /* 两侧留白 */
  position: relative;
  min-height: 100vh;
}

/* 背景图片样式 */
.background-layer {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: url('@/assets/blackbear.png'); /* 修改为你的图片路径 */
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  filter: blur(2px); /* 可选模糊效果 */
  opacity: 0.4; /* 调整透明度 */
  z-index: 1;
}

/* 内容层样式 */
.content-layer {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  z-index: 2; /* 确保内容在背景上方 */
}

/* 卡片样式优化 */
.feature-card {
  background: rgba(255, 255, 255, 0.85); /* 半透明背景 */
  backdrop-filter: blur(5px); /* 毛玻璃效果 */
  border: none;
  transition: all 0.3s ease;
  
  &:hover {
    background: rgba(255, 255, 255, 0.95);
    transform: translateY(-5px);
  }
}

/* 文字可读性增强 */
.text-gray-600 {
  color: rgba(0, 0, 0, 0.7);
}

</style>