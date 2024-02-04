<template>
  <Header />
  <div class="container">
    <Balance />
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
import { ref } from "vue";

const transactions = ref([]);
const totalIncomes = ref(0);
const totalExpenses = ref(0);

const addTransaction = (transaction) => {
  transactions.value.push(transaction);
  getIncome();
  getExpense();
};

const deleteTransaction = (id) => {
  transactions.value = transactions.value.filter((el) => el.id !== id);
  getIncome();
  getExpense();
};

const getIncome = () => {
  const incomes = transactions.value.filter((el) => el.transactionPrice > 0);
  const totalIncome = incomes.reduce((acc, val) => {
    return acc + val.transactionPrice;
  }, 0);

  totalIncomes.value = totalIncome;
};

const getExpense = () => {
  const expenses = transactions.value.filter((el) => el.transactionPrice < 0);
  const totalExpense = expenses.reduce((acc, val) => {
    return acc + val.transactionPrice;
  }, 0);

  totalExpenses.value = totalExpense;
};
</script>

