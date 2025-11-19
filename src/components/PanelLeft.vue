<script setup>
	import { computed } from 'vue';
	import IconLocation from './icons/IconLocation.vue';
	import IconCloud from './icons/weather/IconCloud.vue';
	import IconRain from './icons/weather/IconRain.vue';
	import IconSun from './icons/weather/IconSun.vue';

	const { dayData } = defineProps({
		dayData: Object,
		city: String,
	});

	const formattedDay = computed(() =>
		new Date(dayData.date).toLocaleDateString('ru-RU', { weekday: 'long' })
	);

	const formattedDate = computed(() =>
		new Date(dayData.date)
			.toLocaleDateString('ru-RU', {
				day: 'numeric',
				month: 'long',
				year: 'numeric',
			})
			.replace(' г.', '')
	);

	const weatherCode = computed(() => dayData.day.condition.code);
</script>

<template>
	<div class="left-panel">
		<div class="top">
			<span class="day-week">{{ formattedDay }}</span>
			<span class="day-date">{{ formattedDate }}</span>
			<span class="location">
				<IconLocation />
				{{ city }}
			</span>
		</div>

		<div class="bottom">
			<div class="icon">
				<IconSun v-if="weatherCode <= 1003" :size="95" />
				<IconRain v-if="weatherCode >= 1006 && weatherCode < 1063" :size="95" />
				<IconCloud v-if="weatherCode >= 1063" :size="95" />
			</div>

			<span class="temp">{{ dayData.day.avgtemp_c }} °C</span>
			<span class="weather">{{ dayData.day.condition.text }}</span>
		</div>
	</div>
</template>

<style scoped>
	.left-panel {
		padding: 48px 32px 84px;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		width: 500px;
		height: 680px;
		border-radius: 30px;
		background-image: url('../assets/left.jpg');
		background-repeat: no-repeat;
		background-size: cover;
	}

	.top {
		display: flex;
		flex-direction: column;
	}

	.day-week {
		margin-bottom: 16px;
		font-weight: 700;
		font-size: 37px;
		text-transform: capitalize;
	}

	.day-date {
		margin-bottom: 10px;
		font-weight: 500;
		font-size: 22px;
	}

	.location {
		display: flex;
		align-items: center;
		gap: 8px;
		font-weight: 600;
		font-size: 20px;
	}

	.bottom {
		display: flex;
		flex-direction: column;
	}

	.icon {
		margin: 23px;
	}

	.temp {
		margin-bottom: 13px;
		font-weight: 700;
		font-size: 50px;
	}

	.weather {
		font-weight: 700;
		font-size: 30px;
	}
</style>
