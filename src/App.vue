<template>
  <div id="app">
    <header>
      <div class="container">
        <nav>
            <h1 class="logo">Библиотека рецептов</h1>
          <div class="nav-links" :class="{ active: menuActive }">
            <a href="#" @click.prevent="changePage('home')" :class="{ active: currentPage === 'home' }">
              Главная
            </a>
            <a href="#" @click.prevent="changePage('recipes')" :class="{ active: currentPage === 'recipes' }">
              Все рецепты
            </a>
            <a href="#" @click.prevent="changePage('add')" :class="{ active: currentPage === 'add' }">
              Добавить рецепт
            </a>
          </div>
        </nav>
      </div>
    </header>

    <main class="container">
      <HomePage 
        v-if="currentPage === 'home'" 
        :recipes="recipes"
      />
      
      <RecipeList 
        v-else-if="currentPage === 'recipes'"
        :recipes="recipes"
        @view-recipe="viewRecipe"
      />
      
      <RecipeDetail 
        v-else-if="currentPage === 'detail'"
        :recipe="selectedRecipe"
        @back-to-list="changePage('recipes')"
      />
      
      <AddRecipe 
        v-else-if="currentPage === 'add'"
        @add-recipe="addRecipe"
        @cancel="changePage('recipes')"
      />
      
    </main>

    <footer>
      <div class="container">
        <p>Библиотека рецептов &copy; 2025</p>
      </div>
    </footer>
  </div>
</template>

<script>
import HomePage from './components/HomePage.vue'
import RecipeList from './components/RecipeList.vue'
import RecipeDetail from './components/RecipeDetail.vue'
import AddRecipe from './components/AddRecipe.vue'

export default {
  name: 'App',
  components: {
    HomePage,
    RecipeList,
    RecipeDetail,
    AddRecipe
  },
  data() {
    return {
      currentPage: 'home',
      selectedRecipe: null,
      menuActive: false,
      recipes: [
        {
          id: 1,
          title: 'Паста Карбонара',
          description: 'Классическая итальянская паста с беконом, сыром и яйцом.',
          cookingTime: 30,
          servings: 4,
          category: 'Основное блюдо',
          author: 'Мария Иванова',
          ingredients: [
            '400 г спагетти',
            '200 г бекона или панчетты',
            '4 яичных желтка',
            '100 г пармезана',
            'Соль и черный перец по вкусу',
            '2 зубчика чеснока'
          ],
          instructions: [
            'Отварите спагетти в подсоленной воде согласно инструкции на упаковке.',
            'Обжарьте бекон на сковороде до хрустящей корочки.',
            'В отдельной миске смешайте яичные желтки, тертый пармезан и черный перец.',
            'Слейте воду со спагетти, оставив немного воды от варки.',
            'Смешайте спагетти с беконом, затем добавьте яично-сырную смесь, быстро перемешивая.',
            'Подавайте немедленно, посыпав дополнительным пармезаном.'
          ]
        },
        {
          id: 2,
          title: 'Греческий салат',
          description: 'Свежий и полезный салат с овощами и фетой.',
          cookingTime: 15,
          servings: 2,
          category: 'Салат',
          author: 'Алексей Петров',
          ingredients: [
            '2 помидора',
            '1 огурец',
            '1 красная луковица',
            '1 зеленый перец',
            '100 г сыра фета',
            '10 оливок',
            '2 ст. ложки оливкового масла',
            '1 ч. ложка сушеного орегано',
            'Соль по вкусу'
          ],
          instructions: [
            'Нарежьте помидоры, огурец и перец крупными кубиками.',
            'Тонко нарежьте красный лук.',
            'Сложите все овощи в салатник.',
            'Добавьте оливки и кубики феты.',
            'Заправьте оливковым маслом, посыпьте орегано и солью.',
            'Аккуратно перемешайте и подавайте.'
          ]
        }
      ]
    }
  },
  methods: {
    changePage(page) {
      this.currentPage = page
      this.menuActive = false
    },
    viewRecipe(recipe) {
      this.selectedRecipe = recipe
      this.currentPage = 'detail'
    },
    addRecipe(newRecipe) {
      newRecipe.id = this.recipes.length > 0 
        ? Math.max(...this.recipes.map(r => r.id)) + 1 
        : 1
      
      this.recipes.push({...newRecipe})
      this.changePage('recipes')
      alert('Рецепт успешно добавлен!')
    },
    toggleMenu() {
      this.menuActive = !this.menuActive
    }
  }
}
</script>

<style scoped>
header {
  background-color: #4CAF50;
  color: white;
  padding: 1rem 0;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  display: flex;
  align-items: center;
  gap: 10px;
}
.nav-links {
  display: flex;
  gap: 20px;
}

.nav-links a {
  color: white;
  text-decoration: none;
  padding: 8px 16px;
  border-radius: 4px;
  transition: background-color 0.3s;
  display: flex;
  align-items: center;
  gap: 5px;
}

.nav-links a:hover,
.nav-links a.active {
  background-color: rgba(255, 255, 255, 0.2);
}
footer {
  background-color: #333;
  color: white;
  text-align: center;
  padding: 1.5rem 0;
  margin-top: 2rem;
}

footer p {
  margin: 5px 0;
}
</style>