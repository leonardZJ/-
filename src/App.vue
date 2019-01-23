<template>
	<div>
		<!-- <div v-if="!repoUrl">loading...</div>
		<div v-else>most star repo is <a :href="repoUrl">{{ repoName }}</a></div> -->
		<Header></Header>
		<Section></Section>
	</div>
</template>

<script>
	import Header from './components/header'
	import Section from './components/section'
	import axios from 'axios'

	export default {
		components: {
			Header,Section
		}
/*		data() {
			return {
				repoName: '',
				repoUrl: ''
			}
		},
		mounted: function() {
			let url = 'https://api.github.com/search/repositories?q=v&sort=stars'
			axios.get(url).then(result => {
				let res = result.data.items[0]
				this.repoName = res.name
				this.repoUrl = res.html_url
			}).catch(msg => {
				console.log(msg)
			})
		}*/

	}
</script>

<style>

</style>
