<template>
  <Header />
  <div class="container">
    <Balance :totalBalance="totalBalance" />
    <IncomeExpenses
      :totalIncomes="totalIncomes"
      :totalExpenses="totalExpenses"
    />
    <TransactionList
      :transactions="transactions"
      @delete-transaction="deleteTransaction"
    />
    <AddTransaction @add-transaction="addTransaction" />
  </div>
</template>

<script setup>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";
import { computed, ref } from "vue";

const transactions = ref([]);

const addTransaction = (transaction) => {
  transactions.value.push(transaction);
};

const deleteTransaction = (id) => {
  transactions.value = transactions.value.filter((el) => el.id !== id);
};

const totalIncomes = computed(() => {
  const incomes = transactions.value.filter((el) => el.transactionPrice > 0);
  const totalIncome = incomes.reduce((acc, val) => {
    return acc + val.transactionPrice;
  }, 0);

  return totalIncome;
});

const totalExpenses = computed(() => {
  const expenses = transactions.value.filter((el) => el.transactionPrice < 0);
  const totalExpense = expenses.reduce((acc, val) => {
    return acc + val.transactionPrice;
  }, 0);
  return totalExpense;
});

const totalBalance = computed(() => {
  const total = transactions.value.reduce((acc, val) => {
    return acc + val.transactionPrice;
  }, 0);

  return total;
});
</script>

