<template>
	<div class="container">
		<h1 class="title">Youtube Application</h1>

		<SearchBar @termChange="onTermChange" />

		<!-- Yöntem 2: Direkt inline
<SearchBar @termChange="(term) => console.log('Search term changed:', term)" /> -->
	</div>
</template>

<script>
import SearchBar from "./components/SearchBar.vue";
export default {
	name: "App",
	components: {
		SearchBar,
	},
	methods: {
		onTermChange(term) {
			console.log("Search term changed:", term);
		},
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
