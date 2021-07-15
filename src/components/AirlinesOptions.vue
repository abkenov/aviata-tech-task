<template>
	<div class="airlines-options">
		{{ checkedAirlines }}
		<h2 class="airlines-options__title">Авиакомпании</h2>
		<div class="airlines-options__option">
			<input type="checkbox" name="all" id="all" v-model="isAllChecked" value="isAllChecked" @change="checkAll">
			<label for="all">Все</label>
		</div>
		<div class="airlines-options__option" v-for="[code, airline] of Object.entries(airlines)" :key="code">
			<input type="checkbox" :name="code" :checked="true" :value="code" :id="code" v-model="checkedAirlines" @change="returnCheckedAirlines">
			<label :for="code">{{ airline }}</label>
		</div>
	</div>
</template>

<script>
const data = require('../../src/assets/results.json')

export default {
	name: 'AirlinesOptions',
	data() {
		return {
			airlines: data.airlines,
			checkedAirlines: Object.keys(data.airlines),
			isAllChecked: true,
		}
	},
	methods: {
		checkAll() {
			this.$props.filter()
			this.checkedAirlines.length = 0
			this.isAllChecked ? Object.keys(this.airlines).forEach(airline => this.checkedAirlines.push(airline)) : this.checkedAirlines.length = 0
			this.returnCheckedAirlines()
		},
		returnCheckedAirlines() {
			this.$emit('checkedAirlines', this.checkedAirlines)
		}
	},
	watch: {
		checkedAirlines() {
			if(this.checkedAirlines.length === Object.keys(this.airlines).length) {
				this.isAllChecked = true
			} else {
				this.isAllChecked = false
			}
		}
	},
	emits: ['checkedAirlines'],
	props: ['filter']
}
</script>

<style>

.airlines-options {
	margin: 20px;
	width: 240px;
	height: 320px;
	background: #F5F5F5;
	border-radius: 4px;
	overflow-y: scroll;
}

.airlines-options::-webkit-scrollbar {
  width: 3px;
}

::-webkit-scrollbar-track {
  box-shadow: inset 0 0 5px #E1E1E1;
}

::-webkit-scrollbar-thumb {
  background: grey;
	border-radius: 3px;
	margin-right: 3px;
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
	width: 100%;
	height: 32px;
	display: flex;
	align-items: center;
}

.airlines-options__option:hover {
	background: #EBEBEB;
	cursor: pointer;
}

.airlines-options__option>input {
	margin: 12px;
	border: 1px solid #B9B9B9;
	box-sizing: border-box;
	border-radius: 2px;
	cursor: pointer;
}

.airlines-options__option>label {
	font-family: Open Sans;
	font-style: normal;
	font-weight: normal;
	font-size: 12px;
	line-height: 16px;
	cursor: pointer;
}
</style>