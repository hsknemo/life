<script setup>
import { ref } from 'vue';

// 模拟照片数据
const photos = ref([
  {
    id: 1,
    url: 'https://images.unsplash.com/photo-1522383225653-ed111181a951?auto=format&fit=crop&q=80&w=800&h=600',
    title: '春日樱花',
    date: '2026-03-12'
  },
  {
    id: 2,
    url: 'https://images.unsplash.com/photo-1516035069371-29a1b244cc32?auto=format&fit=crop&q=80&w=800&h=600',
    title: '学习摄影',
    date: '2026-03-10'
  },
  {
    id: 3,
    url: 'https://images.unsplash.com/photo-1493770348161-369560ae357d?auto=format&fit=crop&q=80&w=800&h=600',
    title: '家庭聚餐',
    date: '2026-03-05'
  },
  {
    id: 4,
    url: 'https://images.unsplash.com/photo-1506929562872-bb421503ef21?auto=format&fit=crop&q=80&w=800&h=600',
    title: '山日落',
    date: '2026-03-01'
  },
  {
    id: 5,
    url: 'https://images.unsplash.com/photo-1453614512568-c4024d13c247?auto=format&fit=crop&q=80&w=800&h=600',
    title: '咖啡店',
    date: '2026-02-28'
  },
  {
    id: 6,
    url: 'https://images.unsplash.com/photo-1512820790803-83ca734da794?auto=format&fit=crop&q=80&w=800&h=600',
    title: '书架',
    date: '2026-02-25'
  }
]);
</script>

<template>
  <div class="photo-wall">
    <h2 class="photo-wall-title">照片墙</h2>
    <div class="photo-grid">
      <div
        v-for="photo in photos"
        :key="photo.id"
        class="photo-item"
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
          </div>
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
  color: #000000;
  margin-bottom: 2rem;
  text-align: center;
}

.app.dark-mode .photo-wall-title {
  color: #ffffff;
}

.photo-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 1.5rem;
}

.photo-item {
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  background-color: #ffffff;
}

.app.dark-mode .photo-item {
  background-color: #1e1e1e;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
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
  background: linear-gradient(to top, rgba(0, 0, 0, 0.9), transparent);
  padding: 1.5rem 1rem 1rem;
  color: #ffffff;
  transform: translateY(100%);
  transition: transform 0.3s ease;
}

.photo-item:hover .photo-overlay {
  transform: translateY(0);
}

.photo-title {
  margin: 0;
  font-size: 1.1rem;
  font-weight: 600;
}

.photo-date {
  margin: 0.5rem 0 0;
  font-size: 0.9rem;
  opacity: 0.9;
}

@media (max-width: 768px) {
  .photo-grid {
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: 1rem;
  }

  .photo-wall-title {
    font-size: 1.5rem;
  }
}
</style>
