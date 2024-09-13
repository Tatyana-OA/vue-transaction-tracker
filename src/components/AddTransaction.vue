<template>
  <h3>Add new transaction</h3>
  <form id="form" @submit.prevent="addTransaction">
    <div class="form-control">
      <label for="text">Text</label>
      <input type="text" id="text" v-model="name" placeholder="Enter text..." />
    </div>
    <div class="form-control">
      <label for="amount"
        >Amount <br />
        (negative - expense, positive - income)</label
      >
      <input
        type="text"
        id="amount"
        v-model="amount"
        placeholder="Enter amount..."
      />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>

<script setup>
import { ref } from "vue";
import { useToast } from "vue-toastification";

const name = ref("");
const amount = ref("");

const toast = useToast();

const addTransaction = () => {
  if (isNaN(Number(amount.value))) {
    return toast.error("Amount must be a positive or negative number");
  }
  if (!name.value || !amount.value) {
    return toast.error("Please fill in both fields.");
  }

  name.value = "";
  amount.value = "";
};
</script>
