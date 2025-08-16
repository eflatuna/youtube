<template>
	<form class="search-form" @submit.prevent="handleSubmit">
		<input type="text" class="search-input" v-model="searchTerm" />
		<!-- v-model ile inputa yazilan degeri aliyoruz -->
		<button class="search-btn">Search</button>
	</form>
</template>

<script>
export default {
	emits: ["termChange"], //Disariya olay gönderiliyor
	data() {
		return {
			searchTerm: "", //inputta yazilan deger
		};
	},

	methods: {
		handleSubmit() {
			this.$emit("termChange", this.searchTerm); //olayin adi ve data seklinde gönderilir.Burada data inputta yazilan kelimedir.
			this.searchTerm = ""; //inputu temizliyoruz
		},
	},
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Mozilla+Text&display=swap");
.search-form {
	display: flex;
	margin: 20px 0px;
}

.search-input {
	width: 85%;
	padding: 8px;
	margin-right: 20px;
	border-radius: 20px;
}

.search-btn {
	font-family: "Mozilla Text", sans-serif;
	border: none;
	background: red;
	color: black;
	font-size: 16px;
	border-radius: 20px;
	cursor: pointer;
	width: 15%;
}
</style>
