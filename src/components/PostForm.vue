<template>
	<form @submit.prevent>
		<H3>Create post</H3>
		<my-input v-focus v-model="post.title" class="input" type="text" placeholder="Name" />
		<my-input v-model="post.body" class="input" type="text" placeholder="Text" />
		<my-button class="create-btn" @click="createPost">Create</my-button>
	</form>
</template>

<script>

export default {
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

<style scoped>
.create-btn {
	margin-top: 10px;
	align-self: center;
}

form {
	display: flex;
	flex-direction: column;
}

h3 {
	color: #fff;
}
</style>