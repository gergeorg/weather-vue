<script setup>
	import { computed } from 'vue';
	import IconCloud from './icons/weather/IconCloud.vue';
	import IconRain from './icons/weather/IconRain.vue';
	import IconSun from './icons/weather/IconSun.vue';

	const { weatherCode, temp, date, isActive } = defineProps({
		weatherCode: Number,
		temp: Number,
		date: Date,
		isActive: Boolean,
	});

	const iconColor = computed(() =>
		isActive ? 'var(--color-primary-inverted)' : 'var(--color-primary)'
	);
</script>

<template>
	<li class="day-card">
		<button class="day-button" :class="{ active: isActive }">
			<IconSun v-if="weatherCode <= 1003" :color="iconColor" />
			<IconRain v-if="weatherCode >= 1006 && weatherCode < 1063" :color="iconColor" />
			<IconCloud v-if="weatherCode >= 1063" :color="iconColor" />

			<span class="day-week">{{ date.toLocaleDateString('ru-RU', { weekday: 'short' }) }}</span>
			<span class="day-temp">{{ temp }} °C</span>
		</button>
	</li>
</template>

<style scoped>
	.day-card {
		width: 100%;
	}

	.day-button {
		width: 100%;
		padding: 14px 24px;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		gap: 15px;
		border-radius: 10px;
		box-shadow: 1px 2px 4px 0 var(--color-bg-main);
		background-color: var(--color-bg-card);
		color: var(--color-primary);
		font-size: 20px;
		cursor: pointer;
		border: none;
	}

	.active {
		background-color: var(--color-primary);
		color: var(--color-primary-inverted);
	}

	.day-button:not(.active):hover {
		background-color: #3a434f;
	}

	.day-button:not(.active):focus-visible {
		outline: 1px solid #3a434f;
	}

	.day-week {
		font-weight: 400;
	}

	.day-temp {
		font-weight: 700;
	}
</style>
