<template>
	<nav-bar></nav-bar>
	<div class="app">
		<router-view></router-view>
	</div>
</template>
<script>
import NavBar from '@/components/NavBar';
export default {
	components: {
		NavBar
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