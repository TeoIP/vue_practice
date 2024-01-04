<template>
	<div class="app">
		<h1>Page with posts</h1>
		<div class="app__btns">
			<my-button @click="showDialog">Create Post</my-button>
			<my-select v-model="selectedSort" :options="sortOption" />
		</div>
		<my-dialog v-model:show="dialogVisible"><post-form @create="createPost" /></my-dialog>
		<Post-List :posts="sortedPosts" @remove="removePost" v-if="!isPostsLoading" />
		<div v-else>Loading</div>
	</div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import axios from 'axios';

export default {
	components: {
		PostList, PostForm
	},
	data() {
		return {
			posts: [],
			dialogVisible: false,
			isPostsLoading: false,
			selectedSort: '',
			sortOption: [
				{ value: 'title', name: 'bellow title' },
				{ value: 'body', name: 'bellow body' },
			]
		}
	},
	methods: {
		createPost(post) {
			this.posts.push(post);
			this.dialogVisible = false;
		},
		removePost(post) {
			this.posts = this.posts.filter(p => p.id !== post.id)
		},
		showDialog() {
			this.dialogVisible = true;
		},
		async fetchPosts() {
			try {
				this.isPostsLoading = true;
				const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
				this.posts = response.data;
			} catch (e) {
				alert('Error');
			} finally {
				this.isPostsLoading = false;
			}
		}
	},
	mounted() {
		this.fetchPosts();
	},
	computed: {
		sortedPosts() {
			return [...this.posts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort])
			)
		}
	},
}
</script>

<style>
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
}

.app {
	padding: 15px;
	width: 100%;
	height: 100%;
	background-color: #8BC6EC;
	background-image: linear-gradient(135deg, #8BC6EC 0%, #9599E2 100%);

}

.app__btns {
	display: flex;
	justify-content: space-between;
	margin-top: 15px;
	margin-bottom: 15px;
}
</style>