<template>
	<button class="button" :class="{zero: zero}" @click="$emit('click', button)">
		{{ button.text }}
	</button>
</template>

<script>
export default {
	name: "Button",
	props: {
		button: {
			type: Object
		}
	},
	setup(props) {
		const zero = props.button.text === '0'
		return {zero}
	},
}
</script>

<style scoped lang="scss">
.button {
	width: 65px;
	height: 65px;
	background: #313131;
	border-radius: 100%;
	font-weight: bolder;
	box-sizing: border-box;
	color: #fff;
	font-size: 25px;
	display: flex;
	justify-content: center;
	align-items: center;
	justify-self: center;
	border: none;
	outline: none;
}

.zero {
	grid-column: 1/-3;
	width: 130px;
	border-radius: 25px;
}
</style>