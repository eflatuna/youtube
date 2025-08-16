<template>
	<li><img :src="imageUrl" /></li>
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
