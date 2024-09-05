<template>
  <Header />
  <div class="container">
    <Balance />
    <IncomeExpenses />
    <TransactionList v-bind:transactions="transactions" />
    <AddTransaction />
  </div>
</template>

<script setup>
  import Header from './components/Header.vue'
  import Balance from './components/Balance.vue'
  import IncomeExpenses from './components/IncomeExpenses.vue'
  // passing down transactions array to TransactionList
  import TransactionList from './components/TransactionList.vue'
  import AddTransaction from './components/AddTransaction.vue'

  // used to turn something reactive
  import { ref } from 'vue'

  const transactions = ref([
    {id: 1, text: 'Flowers', amount: -67.91},
    {id: 2, text: 'Salary', amount: 705.44},
    {id: 3, text: 'Book', amount: -24.99},
    {id: 4, text: 'Camera', amount: -2559},
  ])  
</script>