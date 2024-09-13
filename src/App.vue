<template>
  <Header />
  <div class="container">
    <Balance :balance="total" />
    <IncomeExpenses :income="income" :expenses="expenses" />
    <TransactionList :transactions="transactions" />
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
import { ref, computed } from "vue";
import { useToast } from "vue-toastification";
// Reactive value using ref
const transactions = ref([
  { id: 1, name: "Salary", value: 2500 },
  { id: 2, name: "Groceries", value: -150 },
  { id: 3, name: "Car Repair", value: -500 },
  { id: 4, name: "Freelance Project", value: 800 },
  { id: 5, name: "Coffee", value: -30 },
  { id: 6, name: "Investment Return", value: 450 },
  { id: 7, name: "Rent", value: -1200 },
  { id: 8, name: "Gym Membership", value: -50 },
  { id: 9, name: "Bonus", value: 500 },
  { id: 10, name: "Electricity Bill", value: -100 },
]);

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
  const transactionId = transactions.value.length + 1;
  transactions.value.push({ id: transactionId, ...transactionData });
  toast.success("Transaction successfully added.");
};
</script>
