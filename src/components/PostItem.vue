<template>
	<div class="post">
		<div>
			<div><strong>Name:</strong>{{ post.title }}</div>
			<div><strong>Text:</strong>{{ post.body }}</div>
		</div>
		<div class="post__btns">
			<my-button>Delete</my-button>
		</div>
	</div>
</template>

<script>
import MyButton from '@/components/UI/MyButton';
export default {
	components: { MyButton },
	props: {
		post: {
			type: Object,
			required: true,
		}
	}
}
</script>

<style>
.post {
	padding: 15px;
	border-radius: 4px;
	border: 3px solid #448FA3;
	background-color: #02182B;
	color: #fff;
	margin-top: 15px;
	display: flex;
	align-items: center;
	justify-content: space-between;
}
</style>