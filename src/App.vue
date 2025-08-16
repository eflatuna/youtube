<template>
	<div class="container">
		<h1 class="title">Youtube Application</h1>

		<SearchBar @termChange="onTermChange" />
		<VideoList :videos="videos" />

		<!-- Yöntem 2: Direkt inline
<SearchBar @termChange="(term) => console.log('Search term changed:', term)" /> -->
	</div>
</template>

<script>
import SearchBar from "./components/SearchBar.vue";
import VideoList from "./components/VideoList.vue";
import axios from "axios";
export default {
	name: "App",
	components: {
		SearchBar,
		VideoList,
	},
	data() {
		return {
			videos: [],
		};
	},
	methods: {
		onTermChange(searchTerm) {
			axios
				.get("https://www.googleapis.com/youtube/v3/search", {
					params: {
						part: "snippet",
						type: "video",
						key: "AIzaSyBEvtw9QOno06ZSag332l4OnhtEvDv7rRs",
						q: searchTerm,
					},
				})
				.then((response) => {
					// console.log(response);
					this.videos = response.data.items;
				})
				.catch((error) => {
					console.log(error);
				});
		},
	},
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Mozilla+Text:wght@200..700&display=swap");
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
	font-family: "Mozilla Text", sans-serif;
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
