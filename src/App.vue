<template>
  <div id="app">
    <h1>Budget Tracker</h1>
    <BudgetInput v-model="budget" />
    <ExpenseList
      :expenses="expenses"
      :remaining-budget="remainingBudget"
      @add-expense="addExpense"
      @remove-expense="removeExpense"
    />
    <BudgetAdvice
      :budget="budget"
      :total-expenses="totalExpenses"
      :remaining-budget="remainingBudget"
    />
    <MealSuggestion :remaining-budget="remainingBudget" />
  </div>
</template>

<script>
import BudgetInput from './components/BudgetInput.vue';
import ExpenseList from './components/ExpenseList.vue';
import BudgetAdvice from './components/BudgetAdvice.vue';
import MealSuggestion from './components/MealSuggestion.vue';

export default {
  components: { BudgetInput, ExpenseList, BudgetAdvice, MealSuggestion },
  data() {
    return {
      budget: 0,
      expenses: []
    };
  },
  computed: {
    totalExpenses() {
      return this.expenses.reduce((sum, expense) => sum + expense.amount, 0);
    },
    remainingBudget() {
      return this.budget - this.totalExpenses;
    }
  },
  methods: {
    addExpense(expense) {
      this.expenses.push({
        id: Date.now(),
        name: expense.name,
        amount: expense.amount
      });
    },
    removeExpense(id) {
      this.expenses = this.expenses.filter(expense => expense.id !== id);
    }
  }
};
</script>

<style>
#app {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

h1 {
  text-align: center;
  color: #333;
}
</style>
