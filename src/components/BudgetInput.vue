<template>
  <div class="budget-input">
    <h2>Set Your Budget</h2>
    <div class="input-group">
      <span class="currency">$</span>
      <input
        type="number"
        :value="modelValue"
        @input="$emit('update:modelValue', parseFloat($event.target.value) || 0)"
        placeholder="Enter your budget"
        min="0"
        step="0.01"
      />
    </div>
    <p class="budget-display" v-if="modelValue > 0">
      Your budget: <strong>${{ modelValue.toFixed(2) }}</strong>
    </p>
  </div>
</template>

<script>
export default {
  props: {
    modelValue: {
      type: Number,
      default: 0
    }
  },
  emits: ['update:modelValue']
};
</script>

<style scoped>
.budget-input {
  background: #f5f5f5;
  padding: 20px;
  border-radius: 8px;
  margin-bottom: 20px;
}

h2 {
  margin-top: 0;
  color: #333;
}

.input-group {
  display: flex;
  align-items: center;
}

.currency {
  font-size: 1.2em;
  margin-right: 8px;
  color: #666;
}

input {
  flex: 1;
  padding: 10px;
  font-size: 1.1em;
  border: 2px solid #ddd;
  border-radius: 4px;
}

input:focus {
  outline: none;
  border-color: #4CAF50;
}

.budget-display {
  margin-top: 10px;
  color: #4CAF50;
  font-size: 1.1em;
}
</style>
