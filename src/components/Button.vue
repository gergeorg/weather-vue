<script setup></script>

<template>
	<button class="button">
		<slot />
	</button>
</template>

<style scoped>
	.button {
		width: 100%;
		height: 53px;
		display: flex;
		gap: 9px;
		align-items: center;
		justify-content: center;
		padding: 14px;
		border: none;
		border-radius: 10px;
		background: var(--gradient);
		font-family: var(--font);
		font-size: 20px;
		font-weight: 600;
		color: var(--color-primary);
		cursor: pointer;
	}

	.button:hover {
		background: var(--gradient-inverted);
	}
</style>
