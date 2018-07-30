<template>
	<div class="editor-container">
		<textarea :value="input" @input="update"></textarea>
		<div v-html="compiledMarkdown"></div>
	</div>
</template>

<script>
	const marked = require("marked")
	const debounce = require("lodash.debounce")

	module.exports = {
		components: {
		},
		data() {
			return {
				input: "# hello"
			}
		},
		methods: {
			update: debounce(function(e) {
				this.input = e.target.value
			}, 300)
		},
		computed: {
			compiledMarkdown() {
				return marked(this.input, { sanitize: true })
			}
		}
	}
</script>

<style scoped>
	.editor-container {
	}
</style>
