<template>
	<div class="container">
		<h1 class="title">Youtube Application</h1>

		<SearchBar @termChange="onTermChange" />

		<!-- Seçim yapılmadan önce VideoDetail render olmasın -->
		<VideoDetail v-if="selectedVideo" :video="selectedVideo" />

		<div>
			<!-- DİKKAT: videos (çoğul) ve event handler parantezsiz -->
			<VideoList :videos="videos" @videoSelect="onVideoSelect" />
		</div>
	</div>
</template>

<script>
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
							key: "AIzaSyBEvtw9QOno06ZSag332l4OnhtEvDv7rRs", // (Not: API key'i env'e taşıman iyi olur)
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

		onVideoSelect(video) {
			this.selectedVideo = video;
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
