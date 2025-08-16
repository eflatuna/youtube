<template>
	<li>
		<img :src="imageUrl" />
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

<style></style>
