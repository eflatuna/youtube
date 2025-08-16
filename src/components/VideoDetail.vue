<template>
	<div v-if="video">
		<iframe
			:src="videoUrl"
			width="100%"
			height="400"
			frameborder="0"
			allowfullscreen
		></iframe>
		<h4>{{ video.snippet.title }}</h4>
		<h4>{{ video.snippet.description }}</h4>
	</div>
</template>

<script>
export default {
	props: {
		video: {
			type: Object,
			required: true,
		},
	},
	computed: {
		videoUrl() {
			const videoId = this.video?.id?.videoId || this.video?.id;
			return `https://www.youtube.com/embed/${videoId}`;
		},
	},
};
</script>
