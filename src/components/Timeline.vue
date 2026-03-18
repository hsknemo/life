<script setup>
import { ref } from 'vue';

// 模拟生活记录数据
const records = ref([
  {
    id: 1,
    date: '2026-03-12',
    title: '春日赏花',
    content: '今天和朋友一起去公园赏花，看到了美丽的樱花和郁金香，心情非常愉快。我们在公园里漫步，欣赏着各种盛开的花朵，还拍了很多照片。中午在公园附近的咖啡馆休息，聊了很多有趣的话题。这真是一个美好的春日午后。',
    image: 'https://images.unsplash.com/photo-1522383225653-ed111181a951?auto=format&fit=crop&q=80&w=800&h=600',
    images: [
      'https://images.unsplash.com/photo-1522383225653-ed111181a951?auto=format&fit=crop&q=80&w=800&h=600',
      'https://images.unsplash.com/photo-1516035069371-29a1b244cc32?auto=format&fit=crop&q=80&w=800&h=600'
    ],
    location: '中央公园',
    weather: '晴朗'
  },
  {
    id: 2,
    date: '2026-03-10',
    title: '学习新技能',
    content: '开始学习摄影，买了一台新相机，希望能记录更多美好的瞬间。今天第一次尝试拍摄风景照片，虽然还有很多不懂的地方，但是感觉很有趣。我会继续努力学习，提高自己的摄影技巧。',
    image: 'https://images.unsplash.com/photo-1516035069371-29a1b244cc32?auto=format&fit=crop&q=80&w=800&h=600',
    images: [
      'https://images.unsplash.com/photo-1516035069371-29a1b244cc32?auto=format&fit=crop&q=80&w=800&h=600'
    ],
    location: '家中',
    weather: '多云'
  },
  {
    id: 3,
    date: '2026-03-05',
    title: '周末聚餐',
    content: '和家人一起在家做了一顿丰盛的晚餐，大家都很开心。我们准备了很多美食，有红烧肉、清蒸鱼、炒青菜等。饭后大家一起聊天，度过了一个温馨的周末夜晚。',
    image: 'https://images.unsplash.com/photo-1493770348161-369560ae357d?auto=format&fit=crop&q=80&w=800&h=600',
    images: [
      'https://images.unsplash.com/photo-1493770348161-369560ae357d?auto=format&fit=crop&q=80&w=800&h=600',
      'https://images.unsplash.com/photo-1506929562872-bb421503ef21?auto=format&fit=crop&q=80&w=800&h=600'
    ],
    location: '家中',
    weather: '小雨'
  }
]);

// 弹窗状态
const showModal = ref(false);
const selectedRecord = ref(null);

// 打开弹窗
const openModal = (record) => {
  selectedRecord.value = record;
  showModal.value = true;
};

// 关闭弹窗
const closeModal = () => {
  showModal.value = false;
  selectedRecord.value = null;
};
</script>

<template>
  <div class="timeline">
    <h2 class="timeline-title">我们的时间线</h2>
    <div class="timeline-list">
      <div
        v-for="record in records"
        :key="record.id"
        class="timeline-item"
        @click="openModal(record)"
      >
        <div class="timeline-date">{{ record.date }}</div>
        <div class="timeline-content">
          <h3 class="timeline-item-title">{{ record.title }}</h3>
          <p class="timeline-item-text">{{ record.content }}</p>
          <img
            v-if="record.image"
            :src="record.image"
            :alt="record.title"
            class="timeline-item-image"
          />
          <div class="timeline-item-more">点击查看详情 →</div>
        </div>
      </div>
    </div>

    <!-- 弹窗 -->
    <div v-if="showModal" class="modal-overlay" @click="closeModal">
      <div class="modal-content" @click.stop>
        <div class="modal-header">
          <h2 class="modal-title">{{ selectedRecord?.title }}</h2>
          <button class="modal-close" @click="closeModal">×</button>
        </div>
        <div class="modal-body">
          <div class="modal-meta">
            <span class="modal-date">{{ selectedRecord?.date }}</span>
            <span v-if="selectedRecord?.location" class="modal-location">{{ selectedRecord.location }}</span>
            <span v-if="selectedRecord?.weather" class="modal-weather">{{ selectedRecord.weather }}</span>
          </div>
          <div class="modal-text">{{ selectedRecord?.content }}</div>
          <div v-if="selectedRecord?.images && selectedRecord.images.length > 0" class="modal-gallery">
            <img
              v-for="(img, index) in selectedRecord.images"
              :key="index"
              :src="img"
              :alt="`${selectedRecord.title} ${index + 1}`"
              class="modal-image"
            />
          </div>
        </div>
        <div class="modal-footer">
          <button class="modal-button" @click="closeModal">关闭</button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.timeline {
  margin-top: 2rem;
}

.timeline-title {
  font-size: 1.8rem;
  color: var(--primary-color);
  margin-bottom: 2rem;
  text-align: center;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.1);
}

.app.dark-mode .timeline-title {
  color: var(--primary-color);
}

.timeline-list {
  position: relative;
  padding-left: 40px;
}

.timeline-list::before {
  content: '';
  position: absolute;
  left: 15px;
  top: 0;
  bottom: 0;
  width: 2px;
  background-color: var(--secondary-color);
}

.app.dark-mode .timeline-list::before {
  background-color: var(--primary-color);
}

.timeline-item {
  position: relative;
  margin-bottom: 2rem;
  border: 1px solid var(--secondary-color);
  border-radius: 8px;
  padding: 1.5rem;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  background-color: var(--card-bg);
  cursor: pointer;
}

.app.dark-mode .timeline-item {
  border-color: var(--primary-color);
  background-color: var(--card-bg);
}

.timeline-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.app.dark-mode .timeline-item:hover {
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
}

.timeline-item::before {
  content: '';
  position: absolute;
  left: -35px;
  top: 30px;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background-color: var(--primary-color);
  border: 4px solid var(--card-bg);
  z-index: 1;
}

.app.dark-mode .timeline-item::before {
  background-color: var(--primary-color);
  border: 4px solid var(--card-bg);
}

.timeline-date {
  position: absolute;
  right: 1.5rem;
  top: -12px;
  background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
  color: #ffffff;
  padding: 0.3rem 0.8rem;
  border-radius: 12px;
  font-size: 0.9rem;
  font-weight: bold;
  white-space: nowrap;
  z-index: 2;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.app.dark-mode .timeline-date {
  background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
  color: #ffffff;
}

.timeline-content {
  margin-top: 0.5rem;
}

.timeline-item-title {
  font-size: 1.3rem;
  color: var(--primary-color);
  margin-top: 0;
  margin-bottom: 0.5rem;
}

.app.dark-mode .timeline-item-title {
  color: var(--primary-color);
}

.timeline-item-text {
  color: var(--text-light);
  line-height: 1.6;
  margin-bottom: 1rem;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.app.dark-mode .timeline-item-text {
  color: var(--text-light);
}

.timeline-item-image {
  width: 100%;
  max-width: 600px;
  border-radius: 8px;
  margin-top: 1rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.app.dark-mode .timeline-item-image {
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
}

.timeline-item-more {
  color: var(--primary-color);
  font-size: 0.9rem;
  font-weight: 500;
  margin-top: 1rem;
  text-align: right;
}

/* 弹窗样式 */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
  padding: 1rem;
}

.modal-content {
  background-color: var(--card-bg);
  border-radius: 12px;
  max-width: 800px;
  width: 100%;
  max-height: 80vh;
  overflow-y: auto;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
  animation: modalFadeIn 0.3s ease;
}

.app.dark-mode .modal-content {
  background-color: var(--card-bg);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.5rem 2rem;
  border-bottom: 1px solid var(--secondary-color);
  background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
  color: #ffffff;
  border-radius: 12px 12px 0 0;
}

.app.dark-mode .modal-header {
  border-bottom: 1px solid var(--primary-color);
  background: linear-gradient(135deg, #343a40, #495057);
}

.modal-title {
  font-size: 1.5rem;
  font-weight: 600;
  margin: 0;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.2);
}

.modal-close {
  background: none;
  border: none;
  font-size: 2rem;
  color: #ffffff;
  cursor: pointer;
  padding: 0;
  width: 30px;
  height: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  transition: background-color 0.3s ease;
}

.modal-close:hover {
  background-color: rgba(255, 255, 255, 0.2);
}

.modal-body {
  padding: 2rem;
}

.modal-meta {
  display: flex;
  gap: 1rem;
  margin-bottom: 1.5rem;
  font-size: 0.9rem;
  color: var(--text-light);
  flex-wrap: wrap;
}

.modal-date {
  font-weight: 500;
  color: var(--primary-color);
}

.modal-text {
  font-size: 1.1rem;
  line-height: 1.7;
  margin-bottom: 2rem;
  color: var(--text-color);
  white-space: pre-wrap;
}

.app.dark-mode .modal-text {
  color: var(--text-color);
}

.modal-gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1rem;
  margin-top: 1.5rem;
}

.modal-image {
  width: 100%;
  height: 200px;
  object-fit: cover;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
}

.modal-image:hover {
  transform: scale(1.02);
}

.app.dark-mode .modal-image {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
}

.modal-footer {
  padding: 1.5rem 2rem;
  border-top: 1px solid var(--secondary-color);
  display: flex;
  justify-content: flex-end;
}

.app.dark-mode .modal-footer {
  border-top: 1px solid var(--primary-color);
}

.modal-button {
  padding: 0.8rem 1.5rem;
  border: none;
  border-radius: 25px;
  background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
  color: #ffffff;
  font-size: 1rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.3s ease;
}

.modal-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
}

/* 动画 */
@keyframes modalFadeIn {
  from {
    opacity: 0;
    transform: translateY(-20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@media (max-width: 768px) {
  .timeline-list {
    padding-left: 30px;
  }

  .timeline-list::before {
    left: 12px;
  }

  .timeline-item::before {
    left: -28px;
    top: 28px;
    width: 16px;
    height: 16px;
  }

  .timeline-date {
    right: 1rem;
    top: -10px;
    font-size: 0.8rem;
    padding: 0.2rem 0.6rem;
  }

  .timeline-item {
    padding: 1.2rem;
  }

  .timeline-item-title {
    font-size: 1.1rem;
  }

  .modal-content {
    max-height: 90vh;
  }

  .modal-header {
    padding: 1.2rem 1.5rem;
  }

  .modal-body {
    padding: 1.5rem;
  }

  .modal-footer {
    padding: 1.2rem 1.5rem;
  }

  .modal-gallery {
    grid-template-columns: 1fr;
  }

  .modal-image {
    height: 180px;
  }
}
</style>
