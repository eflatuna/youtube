<template>
	<div>
		<ul class="video-list">
			<VideoListItem
				@videoSelect="onVideoSelect()"
				v-for="video in videos"
				:key="video.etag"
				:video="video"
			/>
		</ul>
	</div>
</template>

<script>
import VideoListItem from "./VideoListItem.vue";
export default {
	props: ["videos"],

	components: {
		VideoListItem,
	},
	methods: {
		onVideoSelect(video) {
			this.$emit("videoSelect", video);
		},
	},
};
</script>

<style scoped>
.video-list {
	list-style-type: none;
}
</style>
