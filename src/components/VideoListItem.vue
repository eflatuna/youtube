<template>
	<li class="video-list-item">
		<img :src="imageUrl" class="video-image" />
		<div>{{ video.snippet.title }}</div>
	</li>
</template>

<script>
export default {
	props: ["video"],
	computed: {
		imageUrl() {
			return this.video.snippet.thumbnails.medium.url;
		},
	},
};
</script>

<style>
.video-list-item {
	display: flex;
	align-items: center;
	border: 1px solid green;
	box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
	border-radius: 30px;
	margin: 20px;
}
</style>
