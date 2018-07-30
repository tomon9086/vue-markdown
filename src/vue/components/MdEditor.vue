<template>
	<div class="editor-container">
		<textarea :value="input" @input="update"></textarea>
		<div v-html="compiledMarkdown"></div>
	</div>
</template>

<script>
	const marked = require("marked")

	class Debounce {
		constructor() {
			this._timeoutId = null
			return this
		}
		call(f, ms) {
			if(this._timeoutId !== null) clearTimeout(this._timeoutId)
			this._timeoutId = setTimeout(f, ms)
		}
	}

	const debounce = new Debounce()

	module.exports = {
		components: {
		},
		data() {
			return {
				input: "# hello",
				_updateInterval: 300,
				_lastUpdate: 0
			}
		},
		methods: {
			update(e) {
				debounce.call(() => {
					this.input = e.target.value
					console.log("called!")
				}, 300)
			}
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
