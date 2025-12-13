<template>
  <div class="add-recipe">
    <h2 class="page-title">Добавить новый рецепт</h2>
    
    <div class="card">
      <form @submit.prevent="$emit('add-recipe', newRecipe)">
        <div class="form-group">
          <label for="title">Название рецепта *</label>
          <input type="text" id="title" v-model="newRecipe.title" required>
        </div>
        
        <div class="form-group">
          <label for="description">Описание рецепта *</label>
          <textarea id="description" v-model="newRecipe.description" required></textarea>
        </div>
        
        <div class="form-row">
          <div class="form-group">
            <label for="cookingTime">Время приготовления (минуты) *</label>
            <input type="number" id="cookingTime" v-model="newRecipe.cookingTime" required>
          </div>
          
          <div class="form-group">
            <label for="servings">Количество порций *</label>
            <input type="number" id="servings" v-model="newRecipe.servings" required>
          </div>
        </div>
        
        <div class="form-group">
          <label for="category">Категория</label>
          <select id="category" v-model="newRecipe.category">
            <option value="Основное блюдо">Основное блюдо</option>
            <option value="Закуска">Закуска</option>
            <option value="Салат">Салат</option>
            <option value="Десерт">Десерт</option>
            <option value="Напиток">Напиток</option>
          </select>
        </div>
        
        <div class="form-group">
          <label for="author">Ваше имя *</label>
          <input type="text" id="author" v-model="newRecipe.author" required>
        </div>
        
        <div class="form-group">
          <label>Ингредиенты *</label>
          <div v-for="(ingredient, index) in newRecipe.ingredients" :key="index" class="ingredient-row">
            <input type="text" v-model="newRecipe.ingredients[index]" required>
            <button type="button" class="btn-icon" @click="removeIngredient(index)" v-if="newRecipe.ingredients.length > 1">
              <i class="fas fa-minus"></i>
            </button>
            <button type="button" class="btn-icon" @click="addIngredient" v-if="index === newRecipe.ingredients.length - 1">
              <i class="fas fa-plus"></i>
            </button>
          </div>
        </div>
        
        <div class="form-group">
          <label>Инструкция по приготовлению *</label>
          <div v-for="(step, index) in newRecipe.instructions" :key="index" class="instruction-row">
            <textarea v-model="newRecipe.instructions[index]" required></textarea>
            <button type="button" class="btn-icon" @click="removeInstruction(index)" v-if="newRecipe.instructions.length > 1">
              <i class="fas fa-minus"></i>
            </button>
            <button type="button" class="btn-icon" @click="addInstruction" v-if="index === newRecipe.instructions.length - 1">
              <i class="fas fa-plus"></i>
            </button>
          </div>
        </div>
        
        <div class="button-group">
          <button type="submit" class="btn btn-primary">
            <i class="fas fa-save"></i> Сохранить рецепт
          </button>
          <button type="button" class="btn btn-secondary" @click="$emit('cancel')">
            <i class="fas fa-times"></i> Отмена
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AddRecipe',
  data() {
    return {
      newRecipe: {
        id: null,
        title: '',
        description: '',
        cookingTime: '',
        servings: '',
        category: 'Основное блюдо',
        author: '',
        image: 'https://images.unsplash.com/photo-1565958011703-44f9829ba187?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80',
        ingredients: [''],
        instructions: ['']
      }
    }
  },
  emits: ['add-recipe', 'cancel'],
  methods: {
    addIngredient() {
      this.newRecipe.ingredients.push('')
    },
    removeIngredient(index) {
      this.newRecipe.ingredients.splice(index, 1)
    },
    addInstruction() {
      this.newRecipe.instructions.push('')
    },
    removeInstruction(index) {
      this.newRecipe.instructions.splice(index, 1)
    }
  }
}
</script>

<style scoped>
.form-row {
  display: flex;
  gap: 1rem;
}

.ingredient-row,
.instruction-row {
  display: flex;
  gap: 10px;
  margin-bottom: 10px;
  align-items: flex-start;
}

.ingredient-row input,
.instruction-row textarea {
  flex: 1;
}

.btn-icon {
  padding: 8px 12px;
  background: #f0f0f0;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.btn-icon:hover {
  background: #ddd;
}
</style>