<template>
	<div class="app">
		<div class="calculator">
			<Answer :answer="answer"/>
			<div class="numbers">
				<Button v-for="item in buttons" :button="item" @click="setAnswer"/>
			</div>
		</div>
	</div>
</template>

<script>
import {ref} from "vue";
import Answer from "./components/Answer";
import Button from "./components/Button";

export default {
	name: 'App',
	components: {
		Button,
		Answer
	},
	setup() {
		const buttons = [
			{text: 'C', type: 'function'},
			{text: '+/-', type: 'operation'},
			{text: '%', type: 'operation'},
			{text: '/', type: 'operation'},
			{text: '7', type: 'number'},
			{text: '8', type: 'number'},
			{text: '9', type: 'number'},
			{text: 'X', type: 'operation'},
			{text: '4', type: 'number'},
			{text: '5', type: 'number'},
			{text: '6', type: 'number'},
			{text: '-', type: 'operation'},
			{text: '1', type: 'number'},
			{text: '2', type: 'number'},
			{text: '3', type: 'number'},
			{text: '+', type: 'operation'},
			{text: '0', type: 'number'},
			{text: ',', type: 'number'},
			{text: '=', type: 'operation'}
		]
		let answer = ref('0')
		const setAnswer = (value) => {
			switch (value.type) {
				case ('number'):
					if (answer.value === '0') {
						if (value.text === ',') answer.value = '0.'
						else answer.value = value.text
					} else answer.value += value.text
					break
				case ('function'):
					answer.value = '0'
					break

			}
		}
		return {setAnswer, answer, buttons}
	}
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Prompt&display=swap');

* {
	padding: 0;
	margin: 0;
	font-family: 'Prompt', sans-serif;
}

.app {
	display: flex;
	justify-content: center;
	align-items: center;
	min-height: 100vh;
	-webkit-user-select: none;
	background: #ececec;

	.calculator {
		height: 600px;
		width: 350px;
		background: #000;
		border-radius: 20px;
		display: flex;
		justify-content: center;
		flex-direction: column;
		align-items: center;
		padding-bottom: 20px;
		color: #fff;
		box-sizing: border-box;

		.numbers {
			padding-top: 10px;
			width: min-content;
			display: grid;
			grid-template-columns: repeat(4, 1fr);
			grid-gap: 10px;
		}
	}
}
</style>
