<template>
	<div class="editor-container">
		<textarea :value="input" @input="update"></textarea>
		<div v-html="compiledMarkdown"></div>
	</div>
</template>

<script>
	const MarkdownIt = require("markdown-it")
	const debounce = require("lodash.debounce")

	const md = new MarkdownIt()
	md.use(require("markdown-it-katex"), {"throwOnError" : false, "errorColor" : "#cc0000"})

	module.exports = {
		components: {
		},
		data() {
			return {
				input: "# hello\n$S = \\frac{Q_{rev}}{T}$"
			}
		},
		methods: {
			update: debounce(function(e) {
				this.input = e.target.value
			}, 300)
		},
		computed: {
			compiledMarkdown() {
				// console.log(this.input)
				return md.render(this.input)
			}
		}
	}
</script>

<style scoped>
	.editor-container {
		margin: 0;
		height: 100%;
		/*font-family: "Helvetica Neue", Arial, sans-serif;*/
		color: #333;
	}

	textarea, .editor-container div {
		display: inline-block;
		width: 49%;
		height: 100%;
		vertical-align: top;
		box-sizing: border-box;
		padding: 0 20px;
	}

	textarea {
		border: none;
		border-right: 1px solid #ccc;
		resize: none;
		outline: none;
		background-color: #f6f6f6;
		font-size: 14px;
		/*font-family: "Monaco", courier, monospace;*/
		padding: 20px;
	}

	code {
		color: #f66;
	}
</style>
