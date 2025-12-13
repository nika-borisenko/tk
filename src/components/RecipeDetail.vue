<template>
  <div class="recipe-detail">
    <button class="btn btn-secondary" @click="$emit('back-to-list')">
      <i class="fas fa-arrow-left"></i> Назад к списку
    </button>
    
    <div class="card">
      <h2 class="page-title">{{ recipe.title }}</h2>
      <p>{{ recipe.description }}</p>
      
      <div class="recipe-info">
        <div class="info-item">
          <i class="fas fa-clock"></i>
          <span>Время приготовления: {{ recipe.cookingTime }} минут</span>
        </div>
        <div class="info-item">
          <i class="fas fa-utensils"></i>
          <span>Количество порций: {{ recipe.servings }}</span>
        </div>
        <div class="info-item">
          <i class="fas fa-fire"></i>
          <span>Категория: {{ recipe.category }}</span>
        </div>
        <div class="info-item">
          <i class="fas fa-user"></i>
          <span>Автор: {{ recipe.author }}</span>
        </div>
      </div>
      
      <h3 class="section-title">Ингредиенты</h3>
      <ul class="ingredients-list">
        <li v-for="(ingredient, index) in recipe.ingredients" :key="index">
          {{ ingredient }}
        </li>
      </ul>
      
      <h3 class="section-title">Инструкция по приготовлению</h3>
      <ol class="instructions-list">
        <li v-for="(step, index) in recipe.instructions" :key="index">
          {{ step }}
        </li>
      </ol>
    </div>
  </div>
</template>

<script>
export default {
  name: 'RecipeDetail',
  props: {
    recipe: {
      type: Object,
      required: true
    }
  },
  emits: ['back-to-list']
}
</script>

<style scoped>
.recipe-detail img {
  width: 100%;
  max-height: 400px;
  object-fit: cover;
  border-radius: 8px;
  margin-bottom: 1.5rem;
}

.recipe-info {
  display: flex;
  gap: 2rem;
  margin: 1.5rem 0;
  flex-wrap: wrap;
}

.info-item {
  display: flex;
  align-items: center;
  gap: 8px;
  background-color: #f0f9ff;
  padding: 8px 16px;
  border-radius: 20px;
}

.ingredients-list,
.instructions-list {
  padding-left: 1.5rem;
  margin-bottom: 1.5rem;
}

.ingredients-list li,
.instructions-list li {
  margin-bottom: 0.5rem;
}
</style>