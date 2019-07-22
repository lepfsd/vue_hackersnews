<template>
	<div class="pure-menu pure-menu-horizontal">
		<router-link :to="{ path: '/'}" class="pure-menu-heading pure-menu-link">HackerNews</router-link>
		<ul class="pure-menu-list">
			<li class="pure-menu-item"><router-link :to="{ path: '/single'}" class="pure-menu-link">Upload</router-link></li>
		</ul>
	</div>
</template>

<script>
export default {
	name: 'Navbar'
}
</script>

<style scoped>
	.pure-menu {
		background-color: #E17842;
	}
	.pure-menu a {
		color: white;
	}
</style>

