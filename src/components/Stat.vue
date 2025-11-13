<script setup>
	const { label = 'Не задан', stat } = defineProps({
		label: String,
		stat: String,
	});
</script>

<template>
	<li class="stat">
		<p class="stat-name">{{ label }}</p>
		<p class="stat-value">{{ stat }}</p>
	</li>
</template>

<style scoped>
	.stat {
		display: flex;
		justify-content: space-between;
		gap: 16px;
		font-size: 28px;
	}

	.stat-name {
		margin: 0;
		text-transform: uppercase;
		font-weight: 700;
	}
	.stat-value {
		margin: 0;
		font-family: var(--font);
		font-weight: 500;
	}
</style>
