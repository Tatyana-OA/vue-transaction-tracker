<template>
  <Header @resetTracker="handleResetTracker" />
  <div class="container">
    <Balance :balance="total" />
    <IncomeExpenses :income="income" :expenses="expenses" />
    <TransactionList
      :transactions="transactions"
      @transactionDeleted="handleTransactionDeleted"
    />
    <!-- Listen for custom emitted events, assign function that triggers when event is caught-->
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
  </div>
</template>

<script setup>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";
import { ref, computed, onMounted } from "vue";
import { useToast } from "vue-toastification";

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem("transactions"));
  if (savedTransactions.length > 0) {
    transactions.value = savedTransactions;
  }
});

// Reactive value using ref
const transactions = ref([]);

const toast = useToast();

// Get Total
const total = computed(() => {
  return transactions.value.reduce((acc, curr) => acc + curr.value, 0);
});

// Get Income
const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.value > 0)
    .reduce((acc, curr) => acc + curr.value, 0);
});

// Get Expenses
const expenses = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.value < 0)
    .reduce((acc, curr) => acc + curr.value, 0);
});

const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: Math.floor(Math.random() * 1000000000).toString(),
    ...transactionData,
  });
  handleLocalStorageTransactions();
  toast.success("Transaction successfully added.");
};

const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter((tr) => tr.id !== id);
  handleLocalStorageTransactions();
  toast.success("Transaction successfully deleted.");
};

// Handle Local Storage

const handleLocalStorageTransactions = () => {
  localStorage.setItem("transactions", JSON.stringify(transactions.value));
};

const handleResetTracker = () => {
  transactions.value = [];
  localStorage.clear();
};
</script>
