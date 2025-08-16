<template>
	<div class="container">
		<h1 class="title">Youtube Application</h1>
		<SearchBar />
	</div>
</template>

<script>
import SearchBar from "./components/SearchBar.vue";
export default {
	name: "App",
	components: {
		SearchBar,
	},
};
</script>

<style>
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
}
.container {
	max-width: 1200px;
	width: 100%;
	margin: 50px auto;
}
.title {
	text-align: center;
}
</style>
