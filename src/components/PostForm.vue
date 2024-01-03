<template>
	<form @submit.prevent>
		<H3>Create post</H3>
		<input v-model="post.title" class="input" type="text" placeholder="Name">
		<input v-model="post.body" class="input" type="text" placeholder="Text">
		<my-button @click="createPost" class="btn">Create</my-button>
	</form>
</template>

<script>
import MyButton from '@/components/UI/MyButton';
export default {
	components: { MyButton },
	data() {
		return {
			post: {
				title: '',
				body: ''
			}
		}
	},
	methods: {
		createPost() {
			this.post.id = Date.now();
			this.$emit('create', this.post)
			this.post = {
				title: '',
				body: ''
			}
			this.title = '';
			this.body = '';
		}
	}
}
</script>

<style>
form {
	display: flex;
	flex-direction: column;
}

h3 {
	color: #fff;
}

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