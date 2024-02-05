<script setup>
import Header from '@/components/Header.vue';
import Balance from '@/components/Balance.vue';
import IncomeExpenses from '@/components/IncomeExpenses.vue';
import TransactionList from '@/components/TransactionList.vue';
import AddTransaction from '@/components/AddTransaction.vue';

import { computed, ref } from 'vue';

const transactions = ref([
  { id: 1, text: 'Flowers', amount: -19.99 },
  { id: 2, text: 'Salary', amount: 299.97 },
  { id: 3, text: 'Book', amount: -10.00 },
  { id: 4, text: 'Camera', amount: 150.00 }
]);

// Get total
const total = computed(() => {
  return transactions.value
    .reduce((accumulator, transaction) => {
      return accumulator + transaction.amount;
    }, 0);
});

// Get income
const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((accumulator, transaction) => {
      return accumulator + transaction.amount;
    }, 0).toFixed(2);
});

// Get expenses
const expenses = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((accumulator, transaction) => {
      return accumulator + transaction.amount;
    }, 0).toFixed(2);
});

// Add Transaction
const handleTransactionSubmitted = (transactionData) => {
  console.log(transactionData);
};

</script>

<template>
  <Header></Header>
  <div class="container">
    <Balance :total="+total"></Balance>
    <IncomeExpenses :income="+income" :expenses="+expenses"></IncomeExpenses>
    <TransactionList :transactions="transactions"></TransactionList>
    <AddTransaction @transaction-submitted="handleTransactionSubmitted"></AddTransaction>
  </div>
</template>
