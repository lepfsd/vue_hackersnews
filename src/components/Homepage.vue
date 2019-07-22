<template>
	<div>
		<div class="container">
			<h2>Homepage</h2>
		
			<div v-for="(story, i) in stories" :key="i">
				<h3>{{ story.data.title }}</h3>
				<p>{{ story.data.url }}</p>
				<div class="pure-g">
					<div class="pure-u-1-3"><p>comments: {{ story.data.descendants }}</p></div>
					<div class="pure-u-1-3"><p>score: {{ story.data.score }}</p></div>
				</div>			
			</div>
		</div>
		
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


