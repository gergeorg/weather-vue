<script setup>
	import { onMounted, provide, ref, watch } from 'vue';
	import PanelRight from './components/PanelRight.vue';
	import { API_ENDPOINT, cityProvide } from './const';
	import PanelLeft from './components/PanelLeft.vue';

	const data = ref();
	const error = ref();
	const activeIndex = ref(0);
	const city = ref('Казань');

	provide(cityProvide, city);

	watch(city, () => {
		getCity(city.value);
	});

	onMounted(() => {
		getCity(city.value);
	});

	const getCity = async (city) => {
		const params = new URLSearchParams({
			key: '8fcd994f278445b6827100107251311',
			q: city,
			days: 3,
			lang: 'ru',
		});

		const response = await fetch(`${API_ENDPOINT}forecast.json?${params.toString()}`);
		if (response.status !== 200) {
			error.value = await response.json();
			data.value = null;
			return;
		}
		error.value = null;
		data.value = await response.json();
	};
</script>

<template>
	<main class="main">
		<PanelLeft v-if="data" :day-data="data.forecast.forecastday[activeIndex]" :city />
		<PanelRight :data :error :active-index="activeIndex" @select-index="(i) => (activeIndex = i)" />
	</main>
</template>

<style scoped>
	.main {
		display: flex;
		align-items: center;
		justify-content: center;
	}
</style>
