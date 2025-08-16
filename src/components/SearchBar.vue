<template>
	<form class="search-form">
		<input type="text" class="search-input" />
		<button class="search-btn">Search</button>
	</form>
</template>

<script>
export default {
	name: "SearchBar",
};
</script>

<style scoped>
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
	border: none;
	background: green;
	color: white;
	font-size: 18px;
	border-radius: 20px;
	cursor: pointer;
	width: 15%;
}
</style>
