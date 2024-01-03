<template>
	<button>
		<slot>
		</slot>
	</button>
</template>

<script>
</script>
<style>
.btn {
	margin-top: 10px;
	text-align: center;
	display: flex;
	width: 70px;
	align-items: center;
	justify-content: center;
	outline: 0;
	border: 0;
	cursor: pointer;
	transition: box-shadow 0.15s ease, transform 0.15s ease;
	will-change: box-shadow, transform;
	background: #FCFCFD;
	box-shadow: 0px 2px 4px rgb(45 35 66 / 40%), 0px 7px 13px -3px rgb(45 35 66 / 30%), inset 0px -3px 0px #d6d6e7;
	height: 48px;
	padding: 0 32px;
	font-size: 18px;
	border-radius: 6px;
	color: #36395a;
	transition: box-shadow 0.15s ease, transform 0.15s ease;
}

.btn:hover {
	box-shadow: 0px 4px 8px rgb(45 35 66 / 40%), 0px 7px 13px -3px rgb(45 35 66 / 30%), inset 0px -3px 0px #d6d6e7;
	transform: translateY(-2px);
}

.btn:active {
	box-shadow: inset 0px 3px 7px #d6d6e7;
	transform: translateY(2px);
}
</style>