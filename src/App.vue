<template>
  <Header />
  <div class="container">
    <Balance v-bind:total="+total" />
    <IncomeExpenses v-bind:income="+income" v-bind:expenses="+expenses" />
    <TransactionList v-bind:transactions="transactions" @transactionDeleted="handleTransactionDeleted" />
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
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

  import { useToast } from 'vue-toastification'

  // ref used to turn data reactive
  // computed for calculation
  // onMounted is lifecycle hook, fires off automatically when component mounts - similar to useEffect
  import { ref, computed, onMounted } from 'vue'

  const toast = useToast()

  const transactions = ref([])  

  onMounted(() => {
    // check local storage
    // JSON.parse turns from string to regular array again
    const savedTransactions = JSON.parse(localStorage.getItem(transactions))

    if(savedTransactions) {
      transactions.value = savedTransactions
    }
  })

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

  // add transaction
  const handleTransactionSubmitted = (transactionData) => {
    // from the addTransactions the event comes and then modifies (adds to) the transaction array
    transactions.value.push({
      id: genID(),
      text: transactionData.text,
      amount: transactionData.amount
    })

    saveTransactionToLocalStorage()

    toast.success('Transaction added')
  }

  // helper function to generate ID
  const genID = () => {
    return Math.floor(Math.random() * 1000)
  }

  // function to delete transaction
  const handleTransactionDeleted = (id) => {
    transactions.value = transactions.value.filter((transaction) => transaction.id != id)
    toast.success('Transaction deleted')

    saveTransactionToLocalStorage()
  }

  // save to local storage
  const  saveTransactionToLocalStorage = () => {
    localStorage.setItem('transactions', JSON.stringify(transactions.value))
  }
</script>