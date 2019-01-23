<template>
	<div class="head">
		<div class="iuptBox">
			<span class="bigFont">Search GitHub Users</span><br>
			<input class="inputText" type="text" v-model="searchName">
			<button class="inputTextButton" @click="search">search</button>
		</div>
	</div>
</template>

<script>
	import PubSub from 'pubsub-js'

	export default {
		data() {
			return {
				searchName: ''
			}
		},
		methods: {
			search: function() {
				const searchName = this.searchName.trim()
				if(searchName) {
					PubSub.publish('search',searchName)
				}
			}
		}
	}
</script>

<style>
	.head {
		max-width: 90%;
		min-width: 960px;
		height: 300px;
		background: #eee;
		margin: 0 auto;
		position: relative;
	}
	.iuptBox {
		position: absolute;
		left: 10px;
		bottom: 20px;
	}
	.bigFont {
		font-size: 32px;
	}
	.inputText {
		width: 200px;
		height: 32px;
		font-size: 25px;
	}
	.inputTextButton {
		width: 100px;
		height: 38px;
		font-size: 25px;
	}
</style>