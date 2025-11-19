<script setup>
	import { computed } from 'vue';

	import CitySelect from './CitySelect.vue';
	import Stat from './Stat.vue';
	import Error from './Error.vue';
	import DayCard from './DayCard.vue';

	const { error, data, activeIndex } = defineProps({
		error: Object,
		data: Object,
		activeIndex: Number,
	});

	const emit = defineEmits(['select-index', 'select-city']);

	const errorDisplay = computed(() => {
		return errorMap.get(error?.error?.code);
	});

	const statData = computed(() => {
		if (!data || !data.current) {
			return [];
		}

		return [
			{
				label: 'Влажность',
				stat: data.forecast.forecastday[activeIndex].day.avghumidity + ' %',
			},
			{
				label: 'Вероятность дождя',
				stat: data.forecast.forecastday[activeIndex].day.daily_chance_of_rain + ' %',
			},
			{
				label: 'Ветер',
				stat: data.forecast.forecastday[activeIndex].day.maxwind_kph + ' км/ч',
			},
		];
	});
</script>

<template>
	<div class="right-panel">
		<Error v-if="error" :error="errorDisplay" />

		<div v-if="data && data.current">
			<ul class="stat-list">
				<Stat v-for="item in statData" :key="item.label" v-bind="item" />
			</ul>

			<ul class="days-list">
				<DayCard
					v-for="(item, i) in data.forecast.forecastday"
					:weatherCode="item.day.condition.code"
					:temp="item.day.avgtemp_c"
					:date="new Date(item.date)"
					:key="item.date"
					:isActive="activeIndex == i"
					@click="() => emit('select-index', i)"
				/>
			</ul>
		</div>

		<CitySelect />
	</div>
</template>

<style scoped>
	.right-panel {
		background-color: var(--color-bg-main);
		padding: 60px 50px;
		border-radius: 0 25px 25px 0;
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
