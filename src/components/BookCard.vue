<template>
  <div class="book-card" :class="{ completed: book.completed }">
    <div class="book-info">
      <h3>{{ book.title }}</h3>
      <p class="author">{{ book.author }}</p>
      <span class="genre">{{ book.genre }}</span>
    </div>
    
    <div class="book-actions">
         <button 
    @click="$emit('toggle-favorite', book.id)" 
    class="btn btn-favorite"
    :class="{ 'is-favorite': book.favorite }"
  >
    {{ book.favorite ? '★' : '☆' }}
  </button>
      <div v-if="book.completed" class="rating">
        <span 
          v-for="star in 5" 
          :key="star"
          @click="$emit('rate', star)"
        >
          {{ star <= book.rating ? '★' : '☆' }}
        </span>
      </div>
      
      <button 
        @click="$emit('toggle', book.id)" 
        class="btn btn-primary"
      >
        {{ book.completed ? '✓ Прочитана' : 'Отметить' }}
      </button>
      
      <button 
        @click="$emit('delete', book.id)" 
        class="btn btn-danger"
      >
        🗑
      </button>
    </div>
  </div>
</template>

<script setup>
defineProps(['book'])
defineEmits(['toggle', 'delete', 'rate', 'toggle-favorite'])
</script>

<style scoped>
.book-card {
  background: white;
  border-radius: 8px;
  padding: 16px;
  margin-bottom: 12px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
  display: flex;
  justify-content: space-between;
  align-items: center;
  transition: all 0.3s;
}

.book-card.completed {
  background: #f0f7f0;
  opacity: 0.8;
}

.book-info {
  flex: 1;
}

.book-info h3 {
  margin-bottom: 4px;
  color: #333;
}

.author {
  color: #666;
  font-size: 0.9em;
  margin-bottom: 4px;
}

.genre {
  background: #e0e0e0;
  padding: 2px 8px;
  border-radius: 4px;
  font-size: 0.8em;
}

.book-actions {
  display: flex;
  gap: 8px;
  align-items: center;
}

.rating {
  display: flex;
  gap: 2px;
}

.rating span {
  font-size: 20px;
  cursor: pointer;
  color: gold;
}

.rating span:hover {
  transform: scale(1.2);
}

.btn {
  padding: 8px 12px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.9em;
  transition: background 0.3s;
}

.btn-primary {
  background: #4CAF50;
  color: white;
}

.btn-primary:hover {
  background: #45a049;
}

.btn-secondary {
  background: #2196F3;
  color: white;
}

.btn-secondary:hover {
  background: #1e87db;
}

.btn-danger {
  background: #f44336;
  color: white;
  padding: 8px 12px;
}

.btn-danger:hover {
  background: #da190b;
}
.btn-favorite {
  background: #f8f9fa;
  color: #ffd700;
  border: 1px solid #ffd700;
  padding: 8px 12px;
  font-size: 1.2em;
}

.btn-favorite:hover {
  background: #fff3cd;
  transform: scale(1.1);
}

.btn-favorite.is-favorite {
  background: #ffd700;
  color: #333;
  border-color: #ffd700;
}
</style>