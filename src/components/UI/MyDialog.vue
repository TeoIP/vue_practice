<template>
	<div class="dialog" v-if="show" @click.stop="hideDialog">
		<div @click.stop class="dialog__content">
			<slot>
			</slot>
		</div>
	</div>
</template>
<script>
export default {
	name: 'my-dialog',
	props: {
		show: {
			type: Boolean,
			default: false
		}
	},
	methods: {
		hideDialog() {
			this.$emit('update:show', false)
		}
	}
}
</script>
<style>
.dialog {
	top: 0;
	bottom: 0;
	left: 0;
	right: 0;
	background-color: rgb(0, 0, 0, 0.25);
	position: fixed;
	display: flex;
}

.dialog__content {
	margin: auto;
	background-color: #fff;
	border-radius: 12px;
	min-height: 50px;
	min-width: 300px;
	padding: 25px;
}
</style>