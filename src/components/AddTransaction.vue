<template>
  <h3>Add new transaction</h3>
  <form id="form" @submit.prevent="addTransaction">
    <div class="form-control">
      <label for="text">Text</label>
      <input
        type="text"
        id="text"
        placeholder="Enter text..."
        v-model="transactionText"
      />
    </div>
    <div class="form-control">
      <label for="amount"
        >Amount <br />
        (negative - expense, positive - income)</label
      >
      <input
        type="number"
        id="amount"
        placeholder="Enter amount..."
        v-model="transactionPrice"
      />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>

<script setup>
import { ref } from "vue";
import { uid } from "uid";

const emit = defineEmits(["add-transaction"]);

const transactionText = ref("");
const transactionPrice = ref(null);

const addTransaction = () => {
  if (transactionText.value !== "" && transactionPrice.value !== 0) {
    const transaction = {
      id: uid(),
      transactionText: transactionText.value,
      transactionPrice: transactionPrice.value,
    };

    emit("add-transaction", transaction);
  } else {
    alert("Both Field Are Required");
  }
  transactionText.value = "";
  transactionPrice.value = "";
};
</script>
