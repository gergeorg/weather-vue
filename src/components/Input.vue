<script setup>
	const data = defineModel({ type: String, required: true });
</script>

<template>
	<input v-model="data" class="input" type="text" name="city" />
</template>

<style scoped>
	.input {
		padding: 14px 18px;
		width: 260px;
		height: 53px;
		background-color: var(--color-bg-card);
		font-weight: 400;
		font-size: 18px;
		color: var(--color-primary);
		border: none;
		border-radius: 10px;
		box-shadow: 1px 2px 4px 0 var(--color-bg-main);
	}

	.input::placeholder {
		font-weight: 400;
		font-size: 18px;
		color: var(--color-text-placeholder);
	}
</style>
