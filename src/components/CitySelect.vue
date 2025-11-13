<script setup>
	import { onMounted, ref } from 'vue';
	import Button from './Button.vue';
	import IconLocation from './icons/IconLocation.vue';
	import Input from './Input.vue';

	const emit = defineEmits({
		selectCity(payload) {
			return payload;
		},
	});

	const isEdited = ref(false);
	const city = ref('Kazan');

	onMounted(() => {
		emit('selectCity', city.value);
	});

	const select = () => {
		isEdited.value = false;
		emit('selectCity', city.value);
	};

	const edit = () => {
		isEdited.value = true;
	};
</script>

<template>
	<div class="city-select">
		<div v-if="isEdited" class="city-input">
			<Input v-model="city" @keyup.enter="select()" placeholder="Введите город" />
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
