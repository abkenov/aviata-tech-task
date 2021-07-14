<template>
	<div class="airlines-options">
		<h2 class="airlines-options__title">Авиакомпании</h2>
		<div class="airlines-options__option">
			<input type="checkbox" name="all">
			<label for="all">Все</label>
		</div>
		<div class="airlines-options__option" v-for="airline in airlines" :key="airline">
			<input type="checkbox" :name="airline">
			<label :for="airline">{{ airline }}</label>
		</div>
	</div>
</template>

<script>
const data = require('../../src/assets/results.json')

export default {
	name: 'AirlinesOptions',
	data() {
		return {
			airlines: data.airlines
		}
	}
}
</script>

<style>

.airlines-options {
	width: 240px;
	height: 320px;
	background: #F5F5F5;
	border-radius: 4px;
	overflow-y: scroll;
}

.airlines-options::-webkit-scrollbar {
  width: 2px;
}

::-webkit-scrollbar-thumb {
  background: #E1E1E1;
	border-radius: 2px;
}

.airlines-options__title {
	height: 20px;
	margin: 12px;
	font-family: Open Sans;
	font-style: normal;
	font-weight: bold;
	font-size: 14px;
	line-height: 20px;
}

.airlines-options__option {
	width: 191px;
	height: 32px;
	display: flex;
	align-items: center;
}

.airlines-options__option>input {
	margin: 12px;
	border: 1px solid #B9B9B9;
	box-sizing: border-box;
	border-radius: 2px;
}

.airlines-options__option>label {
	font-family: Open Sans;
	font-style: normal;
	font-weight: normal;
	font-size: 12px;
	line-height: 16px;
}
</style>