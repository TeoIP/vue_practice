<template>
	<div class="app">
		<post-form @create="createPost" />
		<Post-List :posts="posts" />
	</div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";


export default {
	components: {
		PostList, PostForm
	},
	data() {
		return {
			posts: [
				{ id: 1, title: ' MAMAMAMAMAMAMAM', body: ' Lorem ipsum 1' },
				{ id: 2, title: ' IIIII', body: ' Lorem ipsum 2' },
				{ id: 3, title: ' SSSS', body: ' Lorem ipsum3 ' },
			],
		}
	},
	methods: {
		createPost(post) {
			this.posts.push(post);
		}
	}
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
</style>