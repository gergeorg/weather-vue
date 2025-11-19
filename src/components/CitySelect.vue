<script setup>
	import { inject, ref } from 'vue';
	import Button from './Button.vue';
	import IconLocation from './icons/IconLocation.vue';
	import Input from './Input.vue';
	import { cityProvide } from '../const';

	const city = inject(cityProvide);

	const isEdited = ref(false);
	const inputValue = ref(city.value);

	const emit = defineEmits({
		selectCity(payload) {
			return payload;
		},
	});

	const select = () => {
		isEdited.value = false;
		city.value = inputValue.value;
	};

	const edit = () => {
		isEdited.value = true;
	};
</script>

<template>
	<div class="city-select">
		<div v-if="isEdited" class="city-input">
			<Input v-model="inputValue" v-focus @keyup.enter="select()" placeholder="Введите город" />
			<Button @click="select()">Сохранить</Button>
		</div>

		<Button v-else @click="edit()">
			<IconLocation />
			Изменить город
		</Button>
	</div>
</template>

<style scoped>
	.city-select {
		width: 420px;
	}
	.city-input {
		display: flex;
		gap: 12px;
	}
</style>
