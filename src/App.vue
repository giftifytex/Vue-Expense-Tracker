<template>
  <div class="flex flex-col items-center justify-center h-screen w-screen bg-gray-100">
    <div class="w-80 bg-gray-100 drop-shadow-md p-6">
        <Header />
      <div>
        <Balance :total="total"/>
        <IncomeExpense :income="+income" :expenses="+expenses"/>
        <TransactionList :transactions="transactions" @deleteTransaction="handleTransactionDelete"/>
        <AddTransaction @transactionSubmitted="handleTransactionSubmitted"/>
      </div>
    </div>
      
  </div>
  
</template>

<script setup>
  import Header from './components/Header.vue';
  import Balance from './components/Balance.vue';
  import IncomeExpense from './components/IncomeExpense.vue';
  import TransactionList from './components/TransactionList.vue';
  import AddTransaction from './components/AddTransaction.vue';

  import { ref, computed, onMounted } from 'vue';
  import {useToast} from 'vue-toastification';

  const toast = useToast();
  
  const transactions = ref([])
  
  onMounted(() => {
    const savedTransactions = JSON.parse(localStorage.getItem('transactions'));

    if(savedTransactions){
      transactions.value = savedTransactions;
    }
  })
            // Get total
  const total = computed(() => {
    return transactions.value.reduce((acc, transaction) => {
      return acc + transaction.amount;
  }, 0)
  })

// Get Income
const income = computed(() => {
  return transactions.value
  .filter((transaction) => transaction.amount > 0)
  .reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0)
  .toFixed(2);
})
//Get Expense

const expenses = computed(() => {
  return transactions.value
  .filter((transaction) => transaction.amount < 0)
  .reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0).toFixed(2);
})

// Add transactions

const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id:generateUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount,
  })

  saveTransactionsToLocalStorage();
  toast.success('Transaction added successfully')
}

// Generate Unique Id
const generateUniqueId = () => {
  return Math.floor(Math.random() *1000000)
}

// Delete Transaction

const handleTransactionDelete = (transactionId) => {
  transactions.value = transactions.value.filter((transaction) => transaction.id !== transactionId);
  saveTransactionsToLocalStorage();
  toast.success('Transaction Deleted Successfully!');
}


// save to localStoragec

const saveTransactionsToLocalStorage = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value));
}
</script>