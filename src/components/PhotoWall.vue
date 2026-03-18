<script setup>
import { ref } from 'vue';

// 模拟照片数据
const photos = ref([
  {
    id: 1,
    url: 'https://images.unsplash.com/photo-1522383225653-ed111181a951?auto=format&fit=crop&q=80&w=800&h=600',
    title: '春日樱花',
    date: '2026-03-12',
    location: '中央公园',
    description: '在公园里看到了美丽的樱花，粉色的花瓣随风飘落，非常浪漫。',
    camera: 'Canon EOS R5',
    settings: 'f/2.8, 1/200s, ISO 100'
  },
]);
// 弹窗状态
const showModal = ref(false);
const selectedPhoto = ref(null);

// 打开弹窗
const openModal = (photo) => {
  selectedPhoto.value = photo;
  showModal.value = true;
};

// 关闭弹窗
const closeModal = () => {
  showModal.value = false;
  selectedPhoto.value = null;
};
</script>

<template>
  <div class="photo-wall">
    <h2 class="photo-wall-title">我们的照片</h2>
    <div class="photo-grid">
      <div
        v-for="photo in photos"
        :key="photo.id"
        class="photo-item"
        @click="openModal(photo)"
      >
        <div class="photo-container">
          <img
            :src="photo.url"
            :alt="photo.title"
            class="photo-image"
          />
          <div class="photo-overlay">
            <h3 class="photo-title">{{ photo.title }}</h3>
            <p class="photo-date">{{ photo.date }}</p>
            <div class="photo-more">点击查看详情 →</div>
          </div>
        </div>
      </div>
    </div>

    <!-- 弹窗 -->
    <div v-if="showModal" class="modal-overlay" @click="closeModal">
      <div class="modal-content" @click.stop>
        <div class="modal-header">
          <h2 class="modal-title">{{ selectedPhoto?.title }}</h2>
          <button class="modal-close" @click="closeModal">×</button>
        </div>
        <div class="modal-body">
          <div class="modal-image-container">
            <img
              :src="selectedPhoto?.url"
              :alt="selectedPhoto?.title"
              class="modal-image"
            />
          </div>
          <div class="modal-meta">
            <div class="meta-item">
              <span class="meta-label">拍摄日期：</span>
              <span class="meta-value">{{ selectedPhoto?.date }}</span>
            </div>
            <div class="meta-item">
              <span class="meta-label">拍摄地点：</span>
              <span class="meta-value">{{ selectedPhoto?.location }}</span>
            </div>
            <div class="meta-item">
              <span class="meta-label">相机：</span>
              <span class="meta-value">{{ selectedPhoto?.camera }}</span>
            </div>
            <div class="meta-item">
              <span class="meta-label">拍摄参数：</span>
              <span class="meta-value">{{ selectedPhoto?.settings }}</span>
            </div>
          </div>
          <div class="modal-description">
            <h3 class="description-title">照片描述</h3>
            <p class="description-text">{{ selectedPhoto?.description }}</p>
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
.photo-wall {
  margin-top: 2rem;
}

.photo-wall-title {
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

.photo-wall-title::after {
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

.app.dark-mode .photo-wall-title {
  color: var(--primary-color);
}

.photo-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 1.5rem;
}

.photo-item {
  border-radius: 4px;
  overflow: hidden;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  background-color: var(--card-bg);
  border: 2px solid var(--border-color);
  cursor: pointer;
  position: relative;
}

.photo-item::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 3px;
  background: var(--metal-gradient);
}

.app.dark-mode .photo-item {
  background-color: var(--card-bg);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.4);
  border: 2px solid var(--border-color);
}

.app.dark-mode .photo-item::before {
  background: var(--dark-metal-gradient);
}

.photo-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

.app.dark-mode .photo-item:hover {
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.4);
}

.photo-container {
  position: relative;
  aspect-ratio: 4/3;
  overflow: hidden;
}

.photo-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.photo-item:hover .photo-image {
  transform: scale(1.1);
}

.photo-overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(to top, rgba(139, 69, 19, 0.9), rgba(201, 167, 124, 0.7), transparent);
  padding: 1.5rem 1rem 1rem;
  color: #ffffff;
  transform: translateY(100%);
  transition: transform 0.3s ease;
  font-family: 'Courier New', Courier, monospace;
}

.photo-item:hover .photo-overlay {
  transform: translateY(0);
}

.photo-title {
  margin: 0;
  font-size: 1.1rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.photo-date {
  margin: 0.5rem 0 0.5rem;
  font-size: 0.9rem;
  opacity: 0.9;
}

.photo-more {
  font-size: 0.8rem;
  font-weight: 500;
  opacity: 0.9;
  margin-top: 0.5rem;
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
  background: var(--dark-metal-gradient);
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

.modal-image-container {
  margin-bottom: 2rem;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.app.dark-mode .modal-image-container {
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
}

.modal-image {
  width: 100%;
  height: auto;
  object-fit: cover;
}

.modal-meta {
  background-color: rgba(0, 0, 0, 0.05);
  border-radius: 4px;
  padding: 1.5rem;
  margin-bottom: 2rem;
  font-family: 'Courier New', Courier, monospace;
  border-left: 4px solid var(--accent-color);
}

.app.dark-mode .modal-meta {
  background-color: rgba(255, 255, 255, 0.05);
  border-left: 4px solid var(--primary-color);
}

.meta-item {
  display: flex;
  margin-bottom: 0.8rem;
  align-items: flex-start;
}

.meta-item:last-child {
  margin-bottom: 0;
}

.meta-label {
  font-weight: 600;
  color: var(--accent-color);
  min-width: 120px;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.meta-value {
  color: var(--text-color);
  flex: 1;
}

.app.dark-mode .meta-value {
  color: var(--text-color);
}

.modal-description {
  margin-top: 2rem;
}

.description-title {
  font-size: 1.2rem;
  color: var(--accent-color);
  margin-bottom: 1rem;
  font-family: 'Courier New', Courier, monospace;
  text-transform: uppercase;
  letter-spacing: 1px;
  border-bottom: 1px solid var(--border-color);
  padding-bottom: 0.5rem;
}

.description-text {
  font-size: 1.1rem;
  line-height: 1.6;
  color: var(--text-color);
  white-space: pre-wrap;
  font-family: 'Courier New', Courier, monospace;
  background-color: rgba(0, 0, 0, 0.03);
  padding: 1.5rem;
  border-radius: 4px;
  border: 1px solid var(--border-color);
}

.app.dark-mode .description-text {
  color: var(--text-color);
  background-color: rgba(255, 255, 255, 0.03);
  border: 1px solid var(--border-color);
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
  .photo-grid {
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: 1rem;
  }

  .photo-wall-title {
    font-size: 1.5rem;
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

  .meta-item {
    flex-direction: column;
  }

  .meta-label {
    min-width: auto;
    margin-bottom: 0.3rem;
  }
}
</style>
