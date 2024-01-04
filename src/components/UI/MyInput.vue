<template>
	<input :value="modelValue" @input="updateInput" type="text">
</template>
<script>
export default {
	name: 'my-input',
	props: {
		modelValue: [String, Number]
	}
	,
	methods: {
		updateInput(event) {
			this.$emit('update:modelValue', event.target.value)
		}
	}
}
</script>
<style scoped>
.input {
	width: 100%;
	height: 50px;
	outline: none;
	padding: 10px;
	margin-top: 10px;
	border: 3px solid #448FA3;
	color: #fff;
	background-color: #02182B;
}
</style>