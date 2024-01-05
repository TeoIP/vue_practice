<template>
	<div>
		<h1>Page with posts</h1>
		<my-input v-focus class="search" placeholder="Search..." v-model="searchQuery" />
		<div class="app__btns">
			<my-button @click="showDialog">Create Post</my-button>
			<my-select v-model="selectedSort" :options="sortOption" />
		</div>
		<my-dialog v-model:show="dialogVisible"><post-form @create="createPost" /></my-dialog>
		<Post-List :posts="sortedAndSearchedPosts" @remove="removePost" v-if="!isPostsLoading" />
		<div v-else>Loading</div>
		<div v-intersection="loadMorePosts" class="observer"></div>
		<!-- <div class="page__wrapper">
				<div v-for="pageNumber in totalPages" :key="pageNumber" class="page"
					:class="{ 'current-page': page === pageNumber }" @click="changePage(pageNumber)">
					{{ pageNumber }}
				</div>
			</div> -->
	</div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import MyButton from '@/components/UI/MyButton';
import axios from 'axios';
import MySelect from '@/components/UI/MySelect';
import MyInput from '@/components/UI/MyInput';
export default {
	components: {
		PostList, PostForm, MyButton, MyInput, MySelect
	},
	data() {
		return {
			posts: [],
			dialogVisible: false,
			isPostsLoading: false,
			selectedSort: '',
			searchQuery: '',
			page: 1,
			limit: 10,
			totalPages: 0,
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
		// changePage(pageNumber) {
		// 	this.page = pageNumber;
		// },
		async fetchPosts() {
			try {
				this.isPostsLoading = true;
				const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
					params: {
						_page: this.page,
						_limit: this.limit
					}
				});
				this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit);
				this.posts = response.data;
			} catch (e) {
				alert('Error');
			} finally {
				this.isPostsLoading = false;
			}
		},
		async loadMorePosts() {
			try {
				this.page += 1;
				const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
					params: {
						_page: this.page,
						_limit: this.limit
					}
				});
				this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit);
				this.posts = [...this.posts, ...response.data];
			} catch (e) {
				alert('Error');
			}
		}
	},
	mounted() {
		this.fetchPosts();
		console.log(this.$refs.observer);
		// const options = {
		// 	rootMargin: "0px",
		// 	threshold: 1.0,
		// };
		// const callback = (entries, observer) => {
		// 	if (entries[0].isIntersecting && this.page < this.totalPages) {
		// 		this.loadMorePosts()
		// 	}
		// }
		// const observer = new IntersectionObserver(callback, options);
		// observer.observe(this.$refs.observer);
	},
	computed: {
		sortedPosts() {
			return [...this.posts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort])
			)
		},
		sortedAndSearchedPosts() {
			return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
		}
	},
	watch: {
		// page() {
		// 	this.fetchPosts();
		// }
	}
}
</script>

<style>
.app__btns {
	display: flex;
	justify-content: space-between;
	margin-top: 15px;
	margin-bottom: 15px;
}

.page__wrapper {
	display: flex;
	margin-top: 15px;
	gap: 24px;
}

.page {
	border: 1px solid rgb(41, 85, 41);
	padding: 10px;
	color: white;
	background-color: #1c23a0;
}

.current-page {
	background-color: #419241;
	color: black;
}

.search {
	width: 100%;
	height: 50px;
	border: 2px solid black;
	outline: none;
	padding: 10px;
}
</style>