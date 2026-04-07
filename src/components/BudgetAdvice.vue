<template>
  <div class="budget-advice" :class="adviceClass">
    <h2>Budget Advice</h2>
    <div v-if="budget === 0" class="no-budget">
      Enter a budget to get personalized advice!
    </div>
    <div v-else>
      <div class="progress-container">
        <div class="progress-bar" :style="{ width: progressWidth }"></div>
      </div>
      <p class="spending-status">
        You've spent <strong>{{ spentPercentage }}%</strong> of your budget
      </p>
      <div class="advice-message">
        <p>{{ adviceMessage }}</p>
      </div>
      <ul class="tips" v-if="tips.length > 0">
        <li v-for="(tip, index) in tips" :key="index">{{ tip }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    budget: {
      type: Number,
      default: 0
    },
    totalExpenses: {
      type: Number,
      default: 0
    },
    remainingBudget: {
      type: Number,
      default: 0
    }
  },
  computed: {
    spentPercentage() {
      if (this.budget === 0) return 0;
      return Math.min(Math.round((this.totalExpenses / this.budget) * 100), 100);
    },
    progressWidth() {
      return Math.min(this.spentPercentage, 100) + '%';
    },
    adviceClass() {
      if (this.budget === 0) return '';
      if (this.spentPercentage >= 100) return 'over-budget';
      if (this.spentPercentage >= 75) return 'warning';
      if (this.spentPercentage >= 50) return 'caution';
      return 'good';
    },
    adviceMessage() {
      if (this.remainingBudget < 0) {
        return `You're over budget by $${Math.abs(this.remainingBudget).toFixed(2)}! Time to cut back on spending.`;
      }
      if (this.spentPercentage >= 90) {
        return `Only $${this.remainingBudget.toFixed(2)} left! Be very careful with any additional spending.`;
      }
      if (this.spentPercentage >= 75) {
        return `You've used most of your budget. Consider limiting non-essential purchases.`;
      }
      if (this.spentPercentage >= 50) {
        return `You're halfway through your budget. Stay mindful of your spending.`;
      }
      if (this.spentPercentage >= 25) {
        return `Good progress! You still have plenty of budget remaining.`;
      }
      return `Great start! You have $${this.remainingBudget.toFixed(2)} available to spend wisely.`;
    },
    tips() {
      const tips = [];
      if (this.remainingBudget < 0) {
        tips.push('Review your expenses and identify non-essentials to cut');
        tips.push('Consider returning recent purchases if possible');
        tips.push('Avoid using credit cards until back on track');
      } else if (this.spentPercentage >= 75) {
        tips.push('Prioritize essential expenses only');
        tips.push('Look for free alternatives for entertainment');
        tips.push('Cook at home instead of eating out');
      } else if (this.spentPercentage >= 50) {
        tips.push('Track daily spending to stay aware');
        tips.push('Set aside some for unexpected expenses');
      }
      return tips;
    }
  }
};
</script>

<style scoped>
.budget-advice {
  background: #fff;
  padding: 20px;
  border-radius: 8px;
  margin-bottom: 20px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
  border-left: 4px solid #ddd;
}

.budget-advice.good {
  border-left-color: #4CAF50;
}

.budget-advice.caution {
  border-left-color: #FFC107;
}

.budget-advice.warning {
  border-left-color: #FF9800;
}

.budget-advice.over-budget {
  border-left-color: #e74c3c;
  background: #fff5f5;
}

h2 {
  margin-top: 0;
  color: #333;
}

.no-budget {
  color: #999;
  text-align: center;
  padding: 20px;
}

.progress-container {
  background: #e0e0e0;
  border-radius: 10px;
  height: 20px;
  overflow: hidden;
  margin-bottom: 15px;
}

.progress-bar {
  height: 100%;
  background: linear-gradient(90deg, #4CAF50, #8BC34A);
  border-radius: 10px;
  transition: width 0.3s ease;
}

.warning .progress-bar {
  background: linear-gradient(90deg, #FF9800, #FFC107);
}

.over-budget .progress-bar {
  background: linear-gradient(90deg, #e74c3c, #c0392b);
}

.spending-status {
  text-align: center;
  font-size: 1.1em;
  color: #666;
}

.advice-message {
  background: #f9f9f9;
  padding: 15px;
  border-radius: 8px;
  margin: 15px 0;
}

.advice-message p {
  margin: 0;
  color: #333;
}

.tips {
  margin: 0;
  padding-left: 20px;
}

.tips li {
  margin: 8px 0;
  color: #666;
}
</style>
