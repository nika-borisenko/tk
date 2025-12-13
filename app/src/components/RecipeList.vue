<template>
  <div class="recipe-list">
    <h2 class="page-title">Все рецепты</h2>
    
    <div v-if="recipes.length === 0" class="card">
      <p>Пока нет ни одного рецепта. Будьте первым, кто добавит рецепт!</p>
    </div>
    
    <div class="recipe-grid">
      <div v-for="recipe in recipes" :key="recipe.id" 
           class="card recipe-card" 
           @click="$emit('view-recipe', recipe)">
        <h3>{{ recipe.title }}</h3>
        <p>{{ recipe.description.substring(0, 100) }}...</p>
        <div class="recipe-meta">
          <span><i class="fas fa-clock"></i> {{ recipe.cookingTime }} мин.</span>
          <span><i class="fas fa-utensils"></i> {{ recipe.servings }} порций</span>
          <span><i class="fas fa-fire"></i> {{ recipe.category }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'RecipeList',
  props: {
    recipes: {
      type: Array,
      required: true
    }
  },
  emits: ['view-recipe']
}
</script>

<style scoped>
.recipe-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 1.5rem;
}

.recipe-card {
  cursor: pointer;
}

.recipe-card img {
  width: 100%;
  height: 200px;
  object-fit: cover;
  border-radius: 8px;
  margin-bottom: 1rem;
}

.recipe-card h3 {
  margin-bottom: 0.5rem;
  color: #4CAF50;
}

.recipe-meta {
  display: flex;
  justify-content: space-between;
  color: #777;
  font-size: 0.9rem;
  margin-top: 1rem;
}
</style>