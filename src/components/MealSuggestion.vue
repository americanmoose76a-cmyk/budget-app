<template>
  <div class="meal-suggestion">
    <h2>Meal Suggestions</h2>
    <div v-if="remainingBudget <= 0" class="no-budget">
      <p>No budget remaining for meals. Consider reducing other expenses!</p>
    </div>
    <div v-else>
      <p class="budget-info">
        Based on your remaining budget of <strong>${{ remainingBudget.toFixed(2) }}</strong>
      </p>
      <div class="meal-categories">
        <div
          v-for="category in applicableCategories"
          :key="category.name"
          class="meal-category"
          :class="category.class"
        >
          <h3>{{ category.name }}</h3>
          <p class="price-range">{{ category.priceRange }}</p>
          <ul>
            <li v-for="(meal, index) in category.meals" :key="index">
              {{ meal }}
            </li>
          </ul>
        </div>
      </div>
      <div class="tips">
        <h4>Money-Saving Tips:</h4>
        <ul>
          <li v-for="(tip, index) in savingTips" :key="index">{{ tip }}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    remainingBudget: {
      type: Number,
      default: 0
    }
  },
  data() {
    return {
      mealCategories: [
        {
          name: 'Budget Friendly',
          class: 'budget',
          minBudget: 0,
          priceRange: 'Under $5 per meal',
          meals: [
            'Rice and beans with vegetables',
            'Pasta with homemade sauce',
            'Vegetable stir-fry',
            'Oatmeal with fruits',
            'Egg fried rice',
            'Lentil soup'
          ]
        },
        {
          name: 'Moderate',
          class: 'moderate',
          minBudget: 20,
          priceRange: '$5-10 per meal',
          meals: [
            'Grilled chicken salad',
            'Homemade burgers',
            'Fish tacos',
            'Vegetable curry with rice',
            'Pasta with meat sauce',
            'Stuffed peppers'
          ]
        },
        {
          name: 'Comfortable',
          class: 'comfortable',
          minBudget: 50,
          priceRange: '$10-20 per meal',
          meals: [
            'Steak with vegetables',
            'Salmon with asparagus',
            'Shrimp stir-fry',
            'Homemade pizza night',
            'BBQ ribs',
            'Chicken parmesan'
          ]
        },
        {
          name: 'Treat Yourself',
          class: 'treat',
          minBudget: 100,
          priceRange: '$20+ per meal',
          meals: [
            'Restaurant dining',
            'Seafood feast',
            'Premium steakhouse',
            'Sushi dinner',
            'Fine dining experience'
          ]
        }
      ],
      savingTips: [
        'Buy ingredients in bulk when on sale',
        'Plan meals for the week to reduce waste',
        'Cook larger portions and freeze leftovers',
        'Use seasonal vegetables - they\'re cheaper and fresher',
        'Replace meat with beans or lentils some days'
      ]
    };
  },
  computed: {
    applicableCategories() {
      return this.mealCategories.filter(
        category => this.remainingBudget >= category.minBudget
      );
    }
  }
};
</script>

<style scoped>
.meal-suggestion {
  background: #fff;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

h2 {
  margin-top: 0;
  color: #333;
}

.no-budget {
  text-align: center;
  color: #e74c3c;
  padding: 20px;
}

.budget-info {
  text-align: center;
  font-size: 1.1em;
  color: #666;
  margin-bottom: 20px;
}

.meal-categories {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 15px;
  margin-bottom: 20px;
}

.meal-category {
  padding: 15px;
  border-radius: 8px;
  border: 2px solid #ddd;
}

.meal-category.budget {
  border-color: #4CAF50;
  background: #f1f8e9;
}

.meal-category.moderate {
  border-color: #2196F3;
  background: #e3f2fd;
}

.meal-category.comfortable {
  border-color: #FF9800;
  background: #fff3e0;
}

.meal-category.treat {
  border-color: #9C27B0;
  background: #f3e5f5;
}

.meal-category h3 {
  margin: 0 0 5px 0;
  color: #333;
}

.price-range {
  font-size: 0.85em;
  color: #666;
  margin: 0 0 10px 0;
}

.meal-category ul {
  margin: 0;
  padding-left: 18px;
}

.meal-category li {
  margin: 5px 0;
  font-size: 0.9em;
  color: #555;
}

.tips {
  background: #f5f5f5;
  padding: 15px;
  border-radius: 8px;
}

.tips h4 {
  margin: 0 0 10px 0;
  color: #333;
}

.tips ul {
  margin: 0;
  padding-left: 20px;
}

.tips li {
  margin: 5px 0;
  color: #666;
}
</style>
