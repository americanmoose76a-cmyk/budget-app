<template>
  <div>
    <h2>Budget Input</h2>
    <input v-model="budget" placeholder="Enter your budget" />
  </div>
</template>
<script>
export default {
  data() {
    return {
      budget: ''
    };
  }
};
</script>
