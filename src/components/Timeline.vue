<script setup>
import { ref } from 'vue';

// 模拟生活记录数据
const records = ref([
  {
    id: 1,
    date: '2026-03-12',
    title: '春日赏花',
    content: '今天和朋友一起去公园赏花，看到了美丽的樱花和郁金香，心情非常愉快。',
    image: 'https://neeko-copilot.bytedance.net/api/text2image?prompt=beautiful%20cherry%20blossoms%20in%20park&size=800x600'
  },
  {
    id: 2,
    date: '2026-03-10',
    title: '学习新技能',
    content: '开始学习摄影，买了一台新相机，希望能记录更多美好的瞬间。',
    image: 'https://neeko-copilot.bytedance.net/api/text2image?prompt=person%20learning%20photography%20with%20camera&size=800x600'
  },
  {
    id: 3,
    date: '2026-03-05',
    title: '周末聚餐',
    content: '和家人一起在家做了一顿丰盛的晚餐，大家都很开心。',
    image: 'https://neeko-copilot.bytedance.net/api/text2image?prompt=family%20dinner%20at%20home&size=800x600'
  }
]);
</script>

<template>
  <div class="timeline">
    <h2 class="timeline-title">生活时间线</h2>
    <div class="timeline-list">
      <div
        v-for="record in records"
        :key="record.id"
        class="timeline-item"
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
  color: #000000;
  margin-bottom: 2rem;
  text-align: center;
}

.app.dark-mode .timeline-title {
  color: #ffffff;
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
  background-color: #e0e0e0;
}

.app.dark-mode .timeline-list::before {
  background-color: #333333;
}

.timeline-item {
  position: relative;
  margin-bottom: 2rem;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  padding: 1.5rem;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  background-color: transparent;
}

.app.dark-mode .timeline-item {
  border-color: #333333;
  background-color: transparent;
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
  left: -38px;
  top: 30px;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background-color: #000000;
  border: 4px solid #ffffff;
  z-index: 1;
}

.app.dark-mode .timeline-item::before {
  background-color: #ffffff;
  border: 4px solid #121212;
}

.timeline-date {
  position: absolute;
  right: 1.5rem;
  top: -12px;
  background-color: #000000;
  color: #ffffff;
  padding: 0.3rem 0.8rem;
  border-radius: 12px;
  font-size: 0.9rem;
  font-weight: bold;
  white-space: nowrap;
  z-index: 2;
}

.app.dark-mode .timeline-date {
  background-color: #ffffff;
  color: #000000;
}

.timeline-content {
  margin-top: 0.5rem;
}

.timeline-item-title {
  font-size: 1.3rem;
  color: #000000;
  margin-top: 0;
  margin-bottom: 0.5rem;
}

.app.dark-mode .timeline-item-title {
  color: #ffffff;
}

.timeline-item-text {
  color: #333333;
  line-height: 1.6;
  margin-bottom: 1rem;
}

.app.dark-mode .timeline-item-text {
  color: #cccccc;
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
}
</style>
