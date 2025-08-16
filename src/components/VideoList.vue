<template>
	<div>
		<ul class="video-list">
			<VideoListItem
				v-for="v in videos"
				:key="v.id?.videoId || v.etag"
				:video="v"
				@videoSelect="onVideoSelect"
			/>
		</ul>
	</div>
</template>

<script>
import VideoListItem from "./VideoListItem.vue";

export default {
	props: {
		videos: { type: Array, required: true },
	},
	components: { VideoListItem },
	emits: ["videoSelect"],
	methods: {
		onVideoSelect(video) {
			this.$emit("videoSelect", video); // Üste (App.vue) ilet
		},
	},
};
</script>

<style scoped>
.video-list {
	list-style-type: none;
}
</style>
