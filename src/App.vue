<!--
 * @Date: 2020-07-13 20:44:05
 * @Author: dana_chen@sina.cn
 * @LastEditors: dana_chen@sina.cn
 * @LastEditTime: 2020-07-13 22:17:20
 * @FilePath: \codeStudy\github\vue-progress-bar\vue-progress-bar\src\App.vue
-->
<template>
	<div id="app">
		<h5>default</h5>
		<progress-bar
			:completed-steps="completedSteps"
			:total-steps="totalSteps"
			style="width:100%;"
		>
			<template v-slot:footer> </template>
		</progress-bar>
		<h5>width:400,height:40</h5>
		<progress-bar
			:completed-steps="completedSteps"
			:total-steps="totalSteps"
			:height="40"
			:width="400"
		>
		</progress-bar>
	</div>
</template>

<script>
	import ProgressBar from './components/ProgressBar.vue'

	export default {
		name: 'App',
		components: {
			ProgressBar,
		},
		data() {
			return {
				completedSteps: 1,
				totalSteps: 10,
				timer: null,
			}
		},
		methods: {
			startProgress() {
				const self = this
				if (this.timer) {
					window.clearInterval(this.timer)
				}
				this.timer = setInterval(() => {
					if (self.completedSteps === self.totalSteps) self.completedSteps = 0
					self.completedSteps++
				}, 1000)
			},
    },
    mounted() {
      this.startProgress()
    },
	}
</script>

<style>
	#app {
		font-family: Avenir, Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
		color: #2c3e50;
		margin-top: 60px;
	}
</style>
