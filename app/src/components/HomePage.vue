<template>
  <div class="home-page">
    <h2 class="page-title">Добро пожаловать в библиотеку рецептов!</h2>
    
    <div class="card">
      <p>Здесь вы можете найти и поделиться своими рецептами. Здесь уже есть <strong>{{ recipes.length }}</strong> рецепта!</p>
    </div>
    
    <div v-if="recipes.length > 0">
      <h3 class="section-title">Последние рецепты</h3>
      <div class="recipe-grid">
        <div v-for="recipe in recentRecipes" :key="recipe.id" class="card recipe-card">
          <h3>{{ recipe.title }}</h3>
          <p>{{ recipe.description.substring(0, 100) }}...</p>
          <div class="recipe-meta">
            <span><i class="fas fa-clock"></i> {{ recipe.cookingTime }} мин.</span>
            <span><i class="fas fa-utensils"></i> {{ recipe.servings }} порций</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HomePage',
  props: {
    recipes: {
      type: Array,
      required: true
    }
  },
  computed: {
    recentRecipes() {
      return [...this.recipes].slice(0, 3)
    }
  }
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