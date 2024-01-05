<template>
	<div class="navbar">
		<div style="cursor: pointer;" @click="$router.push('/')">Vue 3</div>
		<div class="navbar__btns">
			<my-button @click="$router.push('/posts')">Posts</my-button>
			<my-button @click="$router.push('/about')">About</my-button>
		</div>
	</div>
</template>
<script>
export default {
}
</script>
<style >
.navbar {
	height: 50px;
	background-color: rgb(71, 71, 201);
	box-shadow: 2px 2px 4px gray;
	display: flex;
	align-items: center;
	justify-content: space-between;
	color: #fff;
	padding: 15px;
}

.navbar__btns {
	display: flex;
	gap: 50px;
}
</style>