<script setup>
import AddTransaction from './components/AddTransaction.vue';
import Balance from './components/Balance.vue';
import Header from './components/Header.vue';
import IncomeExpense from './components/IncomeExpense.vue';
import TransactionList from './components/TransactionList.vue';

import { ref,computed,onMounted } from 'vue';
import { useToast } from 'vue-toastification';

const toast = useToast();
const transactions = ref([]);

onMounted(()=>{
  const savedTransactions = JSON.parse(localStorage.getItem("transactions"));

  if(savedTransactions){
    transactions.value = savedTransactions;
  }
})

//Total
const total = computed(()=>{
  return transactions.value.reduce((acc,transaction)=>{
    return acc + transaction.amount;
  }, 0);
});

//Income
const income = computed(()=>{
  return transactions.value.filter((transaction)=>{
    return transaction.amount > 0;
  }).reduce((acc,transaction)=>{
    return acc + transaction.amount;
  },0);
});

//Expense
const expense = computed(()=>{
  return transactions.value.filter((transaction)=>{
    return transaction.amount < 0;
  }).reduce((acc,transaction)=>{
    return acc + transaction.amount;
  },0)
})

//Add Transaction
const handleTransactionSubmitted = (transactionData)=>{
  transactions.value.push({
    id : generateUniqueId(),
    text : transactionData.text,
    amount : transactionData.amount
  });
  saveTransactionsToLocalStorage();
  toast.success("Transaction Added");
}

//Generate unique id
const generateUniqueId = ()=>{
  return Math.floor(Math.random()*10000)
}

//Delete
const handleTransactionDeleted = (id)=>{
  transactions.value = transactions.value.filter
  ((transaction)=>transaction.id != id);
  saveTransactionsToLocalStorage();
  toast.success("Transaction Deleted");
}

//Save to Local Storage
const saveTransactionsToLocalStorage = ()=>{
  localStorage.setItem("transactions",JSON.stringify(transactions.value))
}
</script>

<template>
  <Header/>
  <div class="container">
    <Balance :total="+total"/>
    <IncomeExpense :income="+income" :expense="+expense"/>
    <TransactionList :transactions="transactions"
    @transactionDeleted="handleTransactionDeleted"/>
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted"/>
  </div>
</template>
