<script setup>
import { ref, onMounted } from 'vue'

const name = ref('橘子姐姐')
const showMessage = ref(false)
const balloons = ref([])

onMounted(() => {
  // 创建气球
  for (let i = 0; i < 15; i++) {
    balloons.value.push({
      id: i,
      left: Math.random() * 100,
      delay: Math.random() * 5,
      duration: 8 + Math.random() * 6,
      color: ['#ff6b6b', '#4ecdc4', '#ffe66d', '#a8e6cf', '#ff8b94', '#c7ceea'][Math.floor(Math.random() * 6)]
    })
  }
  
  // 延迟显示祝福语
  setTimeout(() => {
    showMessage.value = true
  }, 300)
})
</script>

<template>
  <div class="birthday-page">
    <!-- 气球背景 -->
    <div class="balloons-container">
      <div
        v-for="balloon in balloons"
        :key="balloon.id"
        class="balloon"
        :style="{
          left: balloon.left + '%',
          animationDelay: balloon.delay + 's',
          animationDuration: balloon.duration + 's',
          backgroundColor: balloon.color
        }"
      >
        <div class="balloon-string"></div>
      </div>
    </div>

    <!-- 主内容 -->
    <div class="content" :class="{ show: showMessage }">
      <div class="cake">🎂</div>
      <h1 class="title">Happy Birthday</h1>
      <p class="name">亲爱的 {{ name }}</p>
      <div class="message">
        <p>愿你新的一岁，</p>
        <p>所求皆如愿，所行皆坦途。</p>
        <p>平安喜乐，万事顺遂。</p>
      </div>
      <div class="signature">—— 你的朋友</div>
    </div>
  </div>
</template>

<style scoped>
.birthday-page {
  min-height: 100vh;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: hidden;
  font-family: 'PingFang SC', 'Microsoft YaHei', sans-serif;
}

/* 气球动画 */
.balloons-container {
  position: absolute;
  inset: 0;
  pointer-events: none;
}

.balloon {
  position: absolute;
  bottom: -120px;
  width: 50px;
  height: 60px;
  border-radius: 50% 50% 50% 50% / 60% 60% 40% 40%;
  animation: float-up linear infinite;
  opacity: 0.8;
}

.balloon::before {
  content: '';
  position: absolute;
  top: 8px;
  left: 12px;
  width: 12px;
  height: 18px;
  background: rgba(255, 255, 255, 0.3);
  border-radius: 50%;
}

.balloon-string {
  position: absolute;
  bottom: -30px;
  left: 50%;
  transform: translateX(-50%);
  width: 1px;
  height: 30px;
  background: rgba(255, 255, 255, 0.5);
}

@keyframes float-up {
  0% {
    transform: translateY(0) rotate(-5deg);
    opacity: 0;
  }
  10% {
    opacity: 0.8;
  }
  90% {
    opacity: 0.8;
  }
  100% {
    transform: translateY(-120vh) rotate(5deg);
    opacity: 0;
  }
}

/* 主内容样式 */
.content {
  text-align: center;
  color: white;
  z-index: 10;
  padding: 40px;
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s ease;
}

.content.show {
  opacity: 1;
  transform: translateY(0);
}

.cake {
  font-size: 80px;
  margin-bottom: 20px;
  animation: bounce 2s ease infinite;
}

@keyframes bounce {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-10px); }
}

.title {
  font-size: 56px;
  font-weight: 300;
  margin: 0 0 20px;
  letter-spacing: 4px;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
}

.name {
  font-size: 32px;
  margin: 0 0 40px;
  font-weight: 500;
}

.message {
  font-size: 20px;
  line-height: 2;
  margin-bottom: 40px;
  opacity: 0.95;
}

.message p {
  margin: 8px 0;
}

.signature {
  font-size: 16px;
  opacity: 0.8;
  font-style: italic;
}

/* 响应式 */
@media (max-width: 768px) {
  .title {
    font-size: 36px;
  }
  
  .name {
    font-size: 24px;
  }
  
  .message {
    font-size: 16px;
  }
  
  .cake {
    font-size: 60px;
  }
}
</style>
