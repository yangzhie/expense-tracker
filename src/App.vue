<template>
  <Header />
  <div class="container">
    <Balance v-bind:total="total" />
    <IncomeExpenses v-bind:income="+income" v-bind:expenses="+expenses" />
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
  // this is the only component where we pass props from child to parent then pass it down again to other components
  import AddTransaction from './components/AddTransaction.vue'

  // used to turn something reactive
  import { ref, computed } from 'vue'

  const transactions = ref([
    {id: 1, text: 'Flowers', amount: -67.91},
    {id: 2, text: 'Salary', amount: 705.44},
    {id: 3, text: 'Book', amount: -24.99},
    {id: 4, text: 'Camera', amount: -2559},
  ])  

  // have to use transactions.value as it is in computed form
  const total = computed(() => {
    return transactions.value.reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0)
  })

  // get income 
  // in the passing down of this, we have to convert to Number form using +
  const income = computed(() => {
    return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0).toFixed(2)
  })

  // get expenses
  const expenses = computed(() => {
    return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0).toFixed(2)
  })
</script>