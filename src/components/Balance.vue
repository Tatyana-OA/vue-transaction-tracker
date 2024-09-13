<template>
  <h4>Your Balance</h4>
  <h1 id="balance">${{ balance.toFixed(2) }}</h1>
</template>

<script setup>
import { defineProps } from "vue";

defineProps({
  balance: {
    type: Number,
    required: true,
  },
});
</script>
