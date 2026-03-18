<script setup>
import { ref } from 'vue';

// 模拟生活记录数据
const records = ref([
  {
    id: 1,
    date: '2026-01-05',
    title: '相识',
    content: `
    一月五号呢，我俩加了微信（抱着试一试的态度）， 同意之后发了一些算是自己的个人介绍吧，当然她也把名字发了过来， 她叫李雪， 乍一听就知道是个 「美女」，当然这是后面才知道的，毕竟貌美如花， 我们说了好多话， 讲了好多故事， 分享了不少事情， 有每天早起的打招呼，也有晚上临别进安全区的互相鼓励， 从五号到今天收录了一些她优秀的品质， 【精通算账， 品行端正， 为人低调， 沉默是金（这个是我对腼腆的评价）】， 虽然她说我30岁， 但是我依旧保留我未过28岁的27年龄， 我再加一些吧， 幽默风趣， 脾气好， 这些又会带来温柔似水， 体贴入微， 叶子落入我平静的湖面， 泛起涟漪， 希望这片叶子， 慢慢漂浮， 不追不赶， 希望飘到彼岸的时候， 被捡起来， 依旧可以看清楚上面写的一行字：如果说彩虹是七种颜色构成的， 那么你一定是五彩嫔纷汇聚的， 好看的颜色， 才能构成好看的你

慢慢漂流吧， 将好看进行到底
    `,
    image: new URL('../assets/xiangyu.png', import.meta.url).toString(),
    images: [
      new URL('../assets/xiangyu.png', import.meta.url).toString(),
    ],
    location: '河南&上海',
    weather: '晴☀️'
  },
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
  color: var(--accent-color);
  margin-bottom: 2rem;
  text-align: center;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.2);
  font-family: 'Courier New', Courier, monospace;
  letter-spacing: 2px;
  text-transform: uppercase;
  position: relative;
  padding-bottom: 1rem;
}

.timeline-title::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 100px;
  height: 3px;
  background: var(--metal-gradient);
  border-radius: 2px;
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
  width: 3px;
  background: var(--metal-gradient);
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.3);
}

.app.dark-mode .timeline-list::before {
  background: var(--metal-gradient);
}

.timeline-item {
  position: relative;
  margin-bottom: 2rem;
  border: 2px solid var(--border-color);
  border-radius: 4px;
  padding: 1.5rem;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  background-color: var(--card-bg);
  cursor: pointer;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  position: relative;
  overflow: hidden;
}

.timeline-item::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 3px;
  background: var(--metal-gradient);
}

.app.dark-mode .timeline-item {
  border-color: var(--border-color);
  background-color: var(--card-bg);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.4);
}

.app.dark-mode .timeline-item::before {
  background: var(--metal-gradient);
}

.timeline-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.app.dark-mode .timeline-item:hover {
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
}

.timeline-item::after {
  content: '';
  position: absolute;
  left: -35px;
  top: 30px;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: var(--metal-gradient);
  border: 3px solid var(--border-color);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
  z-index: 1;
}

.app.dark-mode .timeline-item::after {
  background: var(--metal-gradient);
  border: 3px solid var(--border-color);
}

.timeline-date {
  position: absolute;
  right: 1.5rem;
  top: -12px;
  background: var(--metal-gradient);
  color: #ffffff;
  padding: 0.3rem 0.8rem;
  border-radius: 4px;
  font-size: 0.9rem;
  font-weight: bold;
  white-space: nowrap;
  z-index: 2;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
  font-family: 'Courier New', Courier, monospace;
  border: 1px solid var(--border-color);
}

.app.dark-mode .timeline-date {
  background: var(--metal-gradient);
  color: #ffffff;
  border: 1px solid var(--border-color);
}

.timeline-content {
  margin-top: 0.5rem;
}

.timeline-item-title {
  font-size: 1.3rem;
  color: var(--accent-color);
  margin-top: 0;
  margin-bottom: 0.5rem;
  font-family: 'Courier New', Courier, monospace;
  letter-spacing: 1px;
  text-transform: uppercase;
  border-bottom: 1px solid var(--border-color);
  padding-bottom: 0.5rem;
}

.app.dark-mode .timeline-item-title {
  color: var(--primary-color);
  border-bottom: 1px solid var(--border-color);
}

.timeline-item-text {
  color: var(--text-light);
  line-height: 1.6;
  margin-bottom: 1rem;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
  font-family: 'Courier New', Courier, monospace;
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
  color: var(--accent-color);
  font-size: 0.9rem;
  font-weight: 500;
  margin-top: 1rem;
  text-align: right;
  font-family: 'Courier New', Courier, monospace;
  text-transform: uppercase;
  letter-spacing: 1px;
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
  border-radius: 4px;
  max-width: 800px;
  width: 100%;
  max-height: 80vh;
  overflow-y: auto;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
  animation: modalFadeIn 0.3s ease;
  border: 2px solid var(--border-color);
}

.app.dark-mode .modal-content {
  background-color: var(--card-bg);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.5);
  border: 2px solid var(--border-color);
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.5rem 2rem;
  border-bottom: 3px solid var(--border-color);
  background: var(--metal-gradient);
  color: #ffffff;
  border-radius: 4px 4px 0 0;
  position: relative;
  overflow: hidden;
}

.modal-header::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background:
    linear-gradient(45deg, transparent 49%, rgba(255,255,255,0.1) 50%, transparent 51%),
    linear-gradient(-45deg, transparent 49%, rgba(255,255,255,0.1) 50%, transparent 51%);
  background-size: 20px 20px;
  opacity: 0.3;
}

.app.dark-mode .modal-header {
  border-bottom: 3px solid var(--border-color);
  background: var(--metal-gradient);
}

.modal-title {
  font-size: 1.5rem;
  font-weight: 600;
  margin: 0;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.3);
  font-family: 'Courier New', Courier, monospace;
  letter-spacing: 2px;
  text-transform: uppercase;
  position: relative;
  z-index: 1;
}

.modal-close {
  background: rgba(0, 0, 0, 0.3);
  border: 1px solid rgba(255, 255, 255, 0.3);
  font-size: 1.5rem;
  color: #ffffff;
  cursor: pointer;
  padding: 0;
  width: 30px;
  height: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 4px;
  transition: all 0.3s ease;
  font-family: 'Courier New', Courier, monospace;
  position: relative;
  z-index: 1;
}

.modal-close:hover {
  background-color: rgba(0, 0, 0, 0.5);
  transform: rotate(90deg);
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
  font-family: 'Courier New', Courier, monospace;
  background-color: rgba(0, 0, 0, 0.05);
  padding: 1rem;
  border-radius: 4px;
  border-left: 4px solid var(--accent-color);
}

.app.dark-mode .modal-meta {
  background-color: rgba(255, 255, 255, 0.05);
  border-left: 4px solid var(--primary-color);
}

.modal-date {
  font-weight: 500;
  color: var(--accent-color);
  font-family: 'Courier New', Courier, monospace;
}

.modal-text {
  font-size: 1.1rem;
  line-height: 1.7;
  margin-bottom: 2rem;
  color: var(--text-color);
  white-space: pre-wrap;
  font-family: 'Courier New', Courier, monospace;
  background-color: rgba(0, 0, 0, 0.03);
  padding: 1.5rem;
  border-radius: 4px;
  border: 1px solid var(--border-color);
}

.app.dark-mode .modal-text {
  color: var(--text-color);
  background-color: rgba(255, 255, 255, 0.03);
  border: 1px solid var(--border-color);
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
  border: 2px solid var(--border-color);
  border-radius: 4px;
  background: var(--metal-gradient);
  color: #ffffff;
  font-size: 1rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.3s ease;
  font-family: 'Courier New', Courier, monospace;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.modal-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
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
