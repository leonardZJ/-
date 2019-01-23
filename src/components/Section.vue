<template>
	<div class="imgBoxOut">
		<h2 v-if="searchBefore">请输入要搜索的用户名</h2>
		<div v-if="loading">Loading</div>
		<div v-if="errorMsg">{{ errorMsg }}</div>
		<div v-for="(user,index) in users" :key="index">
			<div class="imgBox">
				<a :href="user.Url">
					<img :src="user.avatar_url">
				</a>
				<p>{{ user.name }}</p>
			</div>
		</div>
	</div>
</template>

<script>
	import PubSub from 'pubsub-js'
	import axios from 'axios'

	export default {
		data() {
			return {
				searchBefore: true,
				loading: false,
				users: null,
				errorMsg: ''
			}
		},
		mounted: function() {
			PubSub.subscribe('search',(msg,searchName) => {
				let requestUrl = `https://api.github.com/search/users?q=${ searchName }`

				this.searchBefore = false
				this.loading = true
				this.users = null
				this.errorMsg = ''

				axios.get(requestUrl).then(response => {
					this.loading = false
					let result = response.data
					this.users = result.items.map(item => ({
						avatar_url: item.avatar_url,
						Url: item.html_url,
						name: item.login
					}))
				}).catch(msg => {
					this.errorMsg = '请求失败'
				})
			})
		}
	}
</script>

<style>
	img {
		height: 200px;
	}
	.imgBox {
		box-sizing:border-box;
		width: 25%;

		border: 1px solid #eee;
		float: left;
		text-align: center;
		padding-top: 5%;
		padding-bottom: 5%;
	}
	.imgBoxOut {
		max-width: 90%;
		min-width: 960px;
		overflow: hidden;
		margin: 0 auto;
	}
</style>