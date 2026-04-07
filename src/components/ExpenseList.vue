<template>
  <div class="expense-list">
    <h2>Expenses</h2>

    <form @submit.prevent="addExpense" class="expense-form">
      <input
        v-model="newExpenseName"
        type="text"
        placeholder="Expense name"
        required
      />
      <div class="amount-input">
        <span class="currency">$</span>
        <input
          v-model.number="newExpenseAmount"
          type="number"
          placeholder="Amount"
          min="0.01"
          step="0.01"
          required
        />
      </div>
      <button type="submit">Add</button>
    </form>

    <div v-if="expenses.length === 0" class="no-expenses">
      No expenses yet. Add one above!
    </div>

    <ul v-else>
      <li v-for="expense in expenses" :key="expense.id">
        <span class="expense-name">{{ expense.name }}</span>
        <span class="expense-amount">${{ expense.amount.toFixed(2) }}</span>
        <button class="delete-btn" @click="$emit('remove-expense', expense.id)">X</button>
      </li>
    </ul>

    <div v-if="expenses.length > 0" class="totals">
      <div class="total-row">
        <span>Total Expenses:</span>
        <span class="total-amount">${{ totalExpenses.toFixed(2) }}</span>
      </div>
      <div class="total-row remaining" :class="{ negative: remainingBudget < 0 }">
        <span>Remaining:</span>
        <span class="total-amount">${{ remainingBudget.toFixed(2) }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    expenses: {
      type: Array,
      default: () => []
    },
    remainingBudget: {
      type: Number,
      default: 0
    }
  },
  emits: ['add-expense', 'remove-expense'],
  data() {
    return {
      newExpenseName: '',
      newExpenseAmount: null
    };
  },
  computed: {
    totalExpenses() {
      return this.expenses.reduce((sum, expense) => sum + expense.amount, 0);
    }
  },
  methods: {
    addExpense() {
      if (this.newExpenseName && this.newExpenseAmount > 0) {
        this.$emit('add-expense', {
          name: this.newExpenseName,
          amount: this.newExpenseAmount
        });
        this.newExpenseName = '';
        this.newExpenseAmount = null;
      }
    }
  }
};
</script>

<style scoped>
.expense-list {
  background: #fff;
  padding: 20px;
  border-radius: 8px;
  margin-bottom: 20px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

h2 {
  margin-top: 0;
  color: #333;
}

.expense-form {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.expense-form input[type="text"] {
  flex: 2;
  padding: 10px;
  border: 2px solid #ddd;
  border-radius: 4px;
}

.amount-input {
  flex: 1;
  display: flex;
  align-items: center;
  border: 2px solid #ddd;
  border-radius: 4px;
  padding-left: 8px;
}

.amount-input .currency {
  color: #666;
}

.amount-input input {
  flex: 1;
  padding: 10px;
  border: none;
  outline: none;
  width: 100%;
}

.expense-form button {
  padding: 10px 20px;
  background: #4CAF50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
}

.expense-form button:hover {
  background: #45a049;
}

.no-expenses {
  text-align: center;
  color: #999;
  padding: 20px;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

li {
  display: flex;
  align-items: center;
  padding: 12px;
  border-bottom: 1px solid #eee;
}

li:last-child {
  border-bottom: none;
}

.expense-name {
  flex: 1;
}

.expense-amount {
  margin-right: 15px;
  font-weight: bold;
  color: #e74c3c;
}

.delete-btn {
  background: #e74c3c;
  color: white;
  border: none;
  border-radius: 50%;
  width: 24px;
  height: 24px;
  cursor: pointer;
  font-size: 12px;
}

.delete-btn:hover {
  background: #c0392b;
}

.totals {
  margin-top: 20px;
  padding-top: 15px;
  border-top: 2px solid #eee;
}

.total-row {
  display: flex;
  justify-content: space-between;
  padding: 8px 0;
  font-size: 1.1em;
}

.total-amount {
  font-weight: bold;
}

.remaining .total-amount {
  color: #4CAF50;
}

.remaining.negative .total-amount {
  color: #e74c3c;
}
</style>
