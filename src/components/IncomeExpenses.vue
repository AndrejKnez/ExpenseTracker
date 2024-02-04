<template>
  <div class="inc-exp-container">
    <div>
      <h4>Income</h4>
      <p id="money-plus" class="money plus">+${{ totalIncomes }}</p>
    </div>
    <div>
      <h4>Expense</h4>
      <p id="money-minus" class="money minus">-${{ totalExpenses }}</p>
    </div>
  </div>
</template>

<script setup>
defineProps({
  totalIncomes: {
    type: String,
    required: true,
  },
  totalExpenses: {
    type: String,
    required: true,
  },
});
</script>
