<template>
	<div class="root-container">
		<MdEditor></MdEditor>
	</div>
</template>

<script>
	const MdEditor = require("./components/MdEditor.vue")

	module.exports = {
		components: {
			MdEditor
		},
		data() {
			return {
			}
		},
		methods: {
		},
		computed: {
		}
	}
</script>

<style scoped>
	.root-container {
		height: 100vh;
		min-height: 100vh;
	}
</style>
