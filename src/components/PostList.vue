<template>
	<div v-show="posts.length > 0">
		<h3>Posts list</h3>
		<TransitionGroup name="list">
			<post-item :key="post.id" @remove="$emit('remove', post)" :post="post" v-for="post in posts" />
		</TransitionGroup>
	</div>
	<h2 v-show="posts.length === 0">Lists of posts are empty</h2>
</template>

<script>
import PostItem from '@/components/PostItem';

export default {
	components: { PostItem },
	props: {
		posts: {
			type: Array,
			required: true
		}
	}
}
</script>

<style>
h2 {
	color: red;
	margin-top: 10px;
}

.list-move,
.list-enter-active,
.list-leave-active {
	transition: all 0.5s ease;
}

.list-enter-from,
.list-leave-to {
	opacity: 0;
	transform: translateX(30px);
}

.list-leave-active {
	position: absolute;
}
</style>