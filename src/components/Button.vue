<script setup></script>

<template>
	<button class="button">
		<span>
			<slot name="icon" />
		</span>
		<slot />
	</button>
</template>

<style scoped>
.button {
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
