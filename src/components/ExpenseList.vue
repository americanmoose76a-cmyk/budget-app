<template>
  <div>
    <h2>Expense List</h2>
    <ul>
      <li v-for="expense in expenses" :key="expense.id">{{ expense.name }}: {{ expense.amount }}</li>
    </ul>
  </div>
</template>
<script>
export default {
  data() {
    return {
      expenses: []
    };
  }
};
</script>
