<template>
	<div class="answer">
		{{answer}}
	</div>
</template>

<script>
export default {
	name: "Answer",
	props: {
		answer: {
			type: String
		}
	},
	setup() {
	}
}
</script>

<style scoped lang="scss">
.answer {
	width: 100%;
	height: 200px;
	padding-right: 60px;
	font-size: 50px;
	display: flex;
	justify-content: flex-end;
	align-items: flex-end;
}
</style>