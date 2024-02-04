<template>
  <h3>History</h3>
  <ul id="list" v-if="transactions.length" class="list">
    <li v-for="transaction in transactions" :key="transaction.id">
      {{ transaction.transactionText }}
      <span>${{ transaction.transactionPrice }}</span
      ><button class="delete-btn">x</button>
    </li>
  </ul>
  <p v-else>No transactions yet</p>
</template>

<script setup>
defineProps({
  transactions: {
    type: Array,
    required: true,
  },
});
</script>
