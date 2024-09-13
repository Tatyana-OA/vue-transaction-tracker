<template>
  <h3>History</h3>
  <ul id="list" class="list">
    <li
      v-for="transaction in transactions"
      :class="transaction.value > 0 ? 'plus' : 'minus'"
      :key="transaction.id"
    >
      {{ transaction.name }} <span>${{ transaction.value }}</span>
      <button class="delete-btn" @click="deleteTransaction(transaction.id)">
        x
      </button>
    </li>
  </ul>
</template>

<!-- Options API Syntax -->
<!-- <script>
export default {
  data() {
    return {
      transactions: [
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
      ],
    };
  },
};
</script> -->

<script setup>
import { defineProps } from "vue";

const emit = defineEmits(["transactionDeleted"]);

const props = defineProps({
  transactions: {
    type: Array,
    required: true,
  },
});

const deleteTransaction = (id) => {
  emit("transactionDeleted", id);
};
</script>
