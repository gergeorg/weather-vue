<script setup>
	import { computed, ref } from 'vue';
	import CitySelect from './components/CitySelect.vue';
	import Stat from './components/Stat.vue';
	import Error from './components/Error.vue';
	import DayCard from './components/DayCard.vue';

	const API_ENDPOINT = 'https://api.weatherapi.com/v1/';
	const errorMap = new Map([[1006, 'Указанный город не найден']]);

	const data = ref();
	const error = ref();

	const errorDisplay = computed(() => {
		return errorMap.get(error?.value?.error?.code);
	});

	const getCity = async (city) => {
		const params = new URLSearchParams({
			key: '8fcd994f278445b6827100107251311',
			q: city,
			days: 3,
		});

		const response = await fetch(`${API_ENDPOINT}forecast.json?${params.toString()}`);
		if (response.status !== 200) {
			error.value = await response.json();
			data.value = null;
			return;
		}
		error.value = null;
		data.value = await response.json();
		console.log(data.value);
	};

	const dataModified = computed(() => {
		return [
			{
				label: 'Влажность',
				stat: data.value.current.humidity + ' %',
			},
			{
				label: 'Осадки',
				stat: data.value.current.precip_mm + ' мм',
			},
			{
				label: 'Ветер',
				stat: data.value.current.wind_kph + ' км/ч',
			},
		];
	});
</script>

<template>
	<main class="main">
		<Error :error="errorDisplay" />
		<div v-if="data">
			<ul class="stat-list">
				<Stat v-for="item in dataModified" :key="item.label" v-bind="item" />
			</ul>

			<ul class="days-list">
				<DayCard
					v-for="item in data.forecast.forecastday"
					:weatherCode="item.day.condition.code"
					:temp="item.day.avgtemp_c"
					:date="new Date(item.date)"
					:key="item.date"
				/>
			</ul>
		</div>

		<CitySelect @select-city="getCity" />
	</main>
</template>

<style scoped>
	.main {
		background-color: var(--color-bg-main);
		padding: 60px 50px;
		border-radius: 25px;
	}

	.stat-list {
		display: flex;
		flex-direction: column;
		gap: 16px;
		margin-bottom: 80px;
	}

	.days-list {
		display: flex;
		gap: 1px;
		margin-bottom: 70px;
	}
</style>
