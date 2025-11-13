<script setup>
	const props = defineProps({
		error: String,
	});
</script>

<template>
	<div v-if="props.error" class="error">{{ props.error }}</div>
</template>

<style scoped>
	.error {
		margin-top: -60px;
		margin-bottom: 60px;
		padding: 14px 52px;
		border-radius: 0 0 25px 25px;
		box-shadow: 1px 2px 4px 0 #222831;
		background-color: var(--color-bg-card);
		text-align: center;
		font-size: 18px;
		color: var(--color-primary);
	}
</style>
