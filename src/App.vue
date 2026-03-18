<script setup>
import { ref, watch } from 'vue';
import Timeline from './components/Timeline.vue';
import PhotoWall from './components/PhotoWall.vue';

const activeTab = ref('timeline');
const isDarkMode = ref(false);

const switchTab = (tab) => {
  activeTab.value = tab;
};

const toggleTheme = () => {
  isDarkMode.value = !isDarkMode.value;
};

// 初始化主题 - 默认白色主题
isDarkMode.value = false;
</script>

<template>
  <div class="app" :class="{ 'dark-mode': isDarkMode }">
    <header class="app-header">
      <div class="header-top">
        <h1>雪❤窝</h1>
        <button class="theme-toggle" @click="toggleTheme" aria-label="切换主题">
          <span v-if="!isDarkMode">🌙</span>
          <span v-else>☀️</span>
        </button>
      </div>
      <p>记录我们的美好时光</p>
      <nav class="app-nav">
        <button
          :class="['nav-btn', { active: activeTab === 'timeline' }]"
          @click="switchTab('timeline')"
        >
          时间线
        </button>
        <button
          :class="['nav-btn', { active: activeTab === 'photo' }]"
          @click="switchTab('photo')"
        >
          照片墙
        </button>
      </nav>
    </header>
    <main class="app-main">
      <Timeline v-if="activeTab === 'timeline'" />
      <PhotoWall v-if="activeTab === 'photo'" />
    </main>
    <footer class="app-footer">
      <p>© 2026 雪❤窝</p>
    </footer>
  </div>
</template>

<style scoped>
.app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  background-color: var(--bg-color);
  color: var(--text-color);
  transition: background-color 0.3s ease, color 0.3s ease;
}

.app.dark-mode {
  background-color: var(--bg-color);
  color: var(--text-color);
}

.app-header {
  background: var(--metal-gradient);
  padding: 2rem;
  text-align: center;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
  transition: background 0.3s ease;
  border-bottom: 3px solid var(--border-color);
}

.app.dark-mode .app-header {
  background: var(--metal-gradient);
  border-bottom: 3px solid var(--border-color);
}

.header-top {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.5rem;
}

.theme-toggle {
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
  padding: 0.5rem;
  border-radius: 50%;
  transition: background-color 0.3s ease;
  color: #ffffff;
}

.theme-toggle:hover {
  background-color: rgba(255, 255, 255, 0.1);
}

.app-header h1 {
  margin: 0;
  font-size: 2.5rem;
  color: #ffffff;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
  font-family: 'Courier New', Courier, monospace;
  letter-spacing: 2px;
  text-transform: uppercase;
  position: relative;
  z-index: 1;
}

.app-header p {
  margin: 0.5rem 0 1.5rem;
  font-size: 1.2rem;
  color: rgba(255, 255, 255, 0.9);
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.3);
  font-family: 'Courier New', Courier, monospace;
  position: relative;
  z-index: 1;
}

.app-nav {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin-top: 1rem;
}

.nav-btn {
  padding: 0.8rem 1.5rem;
  border: 2px solid rgba(255, 255, 255, 0.3);
  border-radius: 4px;
  background-color: rgba(0, 0, 0, 0.1);
  color: #ffffff;
  font-size: 1rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.3s ease;
  font-family: 'Courier New', monospace;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.nav-btn:hover {
  background-color: rgba(255, 255, 255, 0.2);
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
}

.nav-btn.active {
  background-color: #ffffff;
  color: var(--primary-color);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
  border: 2px solid var(--border-color);
}

.app.dark-mode .nav-btn.active {
  background-color: var(--primary-color);
  color: #ffffff;
  border: 2px solid var(--border-color);
}

.app-main {
  flex: 1;
  padding: 2rem;
  max-width: 1200px;
  margin: 0 auto;
  width: 100%;
  background-color: var(--bg-color);
  transition: background-color 0.3s ease;
}

.app.dark-mode .app-main {
  background-color: var(--bg-color);
}

.app-footer {
  background: var(--metal-gradient);
  padding: 1rem;
  text-align: center;
  color: #ffffff;
  margin-top: 2rem;
  transition: background 0.3s ease;
  border-top: 3px solid var(--border-color);
  box-shadow: 0 -4px 12px rgba(0, 0, 0, 0.2);
}

.app.dark-mode .app-footer {
  background: var(--metal-gradient);
  border-top: 3px solid var(--border-color);
}

@media (max-width: 768px) {
  .app-header {
    padding: 1.5rem;
  }

  .header-top {
    flex-direction: column;
    gap: 1rem;
  }

  .app-header h1 {
    font-size: 2rem;
  }

  .app-nav {
    flex-direction: column;
    align-items: center;
  }

  .nav-btn {
    width: 200px;
  }

  .app-main {
    padding: 1rem;
  }
}
</style>
