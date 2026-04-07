<template>
  <div id="app">
    <BudgetInput />
    <ExpenseList />
    <BudgetAdvice />
    <MealSuggestion />
  </div>
</template>
<script>
import BudgetInput from './components/BudgetInput.vue';
import ExpenseList from './components/ExpenseList.vue';
import BudgetAdvice from './components/BudgetAdvice.vue';
import MealSuggestion from './components/MealSuggestion.vue';
export default {
  components: { BudgetInput, ExpenseList, BudgetAdvice, MealSuggestion }
};
</script>
