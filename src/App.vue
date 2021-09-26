<template>
	<div class="app">
		<div class="calculator">
			<Answer :answer="answerView"/>
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
			{text: '', type: 'point'},
			{text: '=', type: 'operation'}
		]
		let answer = ref('0')
		let answerView = ref('0')
		const isFirstSymbol = () => {
			return answer.value === '0'
		}
		const isInclude = (symbol) => {
			return (answer.value.split(' ').includes(symbol))
		}
		const count = () => {
			let a = +answer.value.split(' ')[0]
			let b = +answer.value.split(' ')[2]

			if (isInclude('+')) {
				answer.value = (a + b).toString()
			}
			if (isInclude('-')) {
				answer.value = (a - b).toString()
			}

		}
		const setAnswer = (value) => {
			switch (value.type) {
				case ('number'):
					answer.value = isFirstSymbol() ? value.text : answer.value + value.text
					answerView.value = answer.value
					break
				case ('function'):
					answer.value = '0'
					answerView.value = answer.value
					break
				case ('operation'):
					switch (value.text) {
						case ('+/-'):
							if (isFirstSymbol()) answer.value = '-'
							else if (answer.value[0] !== '-') `-${answer.value}`
							answerView.value = answer.value
							break
						case ('%'):
							break
						case ('+'):
							count()
							if (!isFirstSymbol()) answer.value += ' + '
							answerView.value = answer.value
							break
						case ('-'):
							count()
							if (!isFirstSymbol()) answer.value += ' - '
							answerView.value = answer.value
							break
						case ('='):
							count()
							answerView.value = answer.value
							break
					}
			}
		}
		return {setAnswer, answer, buttons, answerView}
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
