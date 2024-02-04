<template>
  <h2>YOUR BALANCE</h2>
  <h1 id="balance">${{ totalBalance }}</h1>
</template>

<script setup>
defineProps({
  totalBalance: {
    type: Number,
    required: true,
  },
});
</script>
