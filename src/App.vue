<script setup>
import { ref } from "vue";
const currentDate = ref(new Date().toLocaleString());
</script>

<template>
	<div>{{ currentDate }}</div>
</template>

<style scoped></style>
