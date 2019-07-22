<template>
	<div>
		<h2>Homepage</h2>
		<div v-for="(story, i) in stories" :key="i">{{ story }}</div>
	</div>
</template>

<script>

import axios from 'axios'

export default {
	name: 'Homepage',
	data: function() {
		return {
			err: '',
			stories: []
		}
	},
	created: function() {
		axios.get('https://hacker-news.firebaseio.com/v0/topstories.json')
			.then((response) => {
				let results = response.data.slice(0, 10)
				results.forEach(id => {
					axios.get('https://hacker-news.firebaseio.com/v0/item/' + id + '.json')
						.then((response) => {
							this.stories.push(response)
						})
						.catch((err) => {
							this.err = err
						})
				})
			})
			.catch((err) => {
				this.err = err;
			})
	}
}
</script>

<style scoped>

</style>


