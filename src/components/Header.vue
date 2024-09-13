<template>
  <div class="tracker">
    <h2>Expense Tracker</h2>
    <button class="btn reset" @click="reset">Reset Tracker</button>
  </div>
</template>

<script setup>
const emit = defineEmits(["resetTracker"]);

const reset = () => {
  emit("resetTracker");
};
</script>
