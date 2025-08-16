<template>
	<li class="video-list-item" @click="onVideoSelect()">
		<img :src="imageUrl" class="video-image" />
		<div>{{ video.snippet.title }}</div>
	</li>
</template>

<script>
export default {
	props: ["video"],
	emits: ["videoSelect"],
	computed: {
		imageUrl() {
			return this.video.snippet.thumbnails.medium.url;
		},
	},
	methods: {
		onVideoSelect() {
			this.$emit("videoSelect", this.video);
		},
	},
};
</script>

<style>
.video-list-item {
	display: flex;
	align-items: center;
	border: 1px solid red;
	box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
	border-radius: 30px;
	margin: 20px;
}

.video-image {
	border-radius: 30px 0px 0px 30px;
	margin-right: 30px;
}
</style>
