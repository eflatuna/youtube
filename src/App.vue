<template>
	<div class="container">
		<h1 class="title">Youtube Application</h1>

		<SearchBar @termChange="onTermChange" />

		<!-- Seçim yapılmadan önce VideoDetail render olmasın -->
		<div ref="detailTop">
			<VideoDetail v-if="selectedVideo" :video="selectedVideo" />
		</div>

		<div>
			<!-- DİKKAT: videos (çoğul) ve event handler parantezsiz -->
			<VideoList :videos="videos" @videoSelect="onVideoSelect" />
		</div>
	</div>
</template>

<script>
import { nextTick } from "vue";
import SearchBar from "./components/SearchBar.vue";
import VideoList from "./components/VideoList.vue";
import VideoDetail from "./components/VideoDetail.vue";
import axios from "axios";

export default {
	name: "App",
	components: { SearchBar, VideoList, VideoDetail },

	data() {
		return {
			videos: [], // Dizi adı çoğul
			selectedVideo: null, // Detayda gösterilecek tekil
		};
	},

	methods: {
		async onTermChange(searchTerm) {
			try {
				const { data } = await axios.get(
					"https://www.googleapis.com/youtube/v3/search",
					{
						params: {
							part: "snippet",
							type: "video",
							maxResults: 10,
							key: "AIzaSyBEvtw9QOno06ZSag332l4OnhtEvDv7rRs",
							q: searchTerm,
						},
					}
				);

				this.videos = data.items || [];
				// Liste boş değilse ilk videoyu seç
				this.selectedVideo = this.videos.length ? this.videos[0] : null;
			} catch (err) {
				console.error("YouTube API error:", err);
				this.videos = [];
				this.selectedVideo = null;
			}
		},

		async onVideoSelect(video) {
			this.selectedVideo = video;
			// VideoDetail DOM’a yerleşsin:
			await nextTick();
			// Sonra yukarı kaydır:
			this.$refs.detailTop?.scrollIntoView({
				behavior: "smooth",
				block: "start",
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
html {
	scroll-behavior: smooth;
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
