<template>
	<div class="guide whatsNew">
		<p class="title">What's new</p>
		<div v-html="whatsNew"></div>
		<div class="custom-block aside">
			<p>
				View the full release
				<a href="https://github.com/inorichi/tachiyomi/releases/latest" target="_blank" rel="noopener">here</a>
			</p>
		</div>
	</div>
</template>

<script>
import marked from "marked";

export default {
	data() {
		return {
			whatsNew: "Failed to load data from GitHub.",
		};
	},

	async mounted() {
		try {
			const { data } = await this.$store.dispatch("getStableReleaseData");
			this.$data.whatsNew = marked(data.body);
		} catch (e) {
			console.error(e);
		}
	},
};
</script>

<style lang="stylus">
.whatsNew
	.title
		text-align center
	div
		white-space
		h3
			font-size 1.1rem
</style>
