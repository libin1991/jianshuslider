<template>
	<div id="app">
		<slider />
	</div>
</template>

<script>
	import slider from './slider.vue'
	export default {
		name: 'app',
		data() {
			return {

			}
		},
		mounted() {
			
		},
		components: {
			slider
		}
	}
</script>

<style lang="scss">
html, body{
	height: 100%;
	width: 100%;
	overflow: hidden;
}
	#app {
	  font-family: "Avenir", Helvetica, Arial, sans-serif;
	  -webkit-font-smoothing: antialiased;
	  -moz-osx-font-smoothing: grayscale;
	  text-align: center;
	  color: #2c3e50;
	  margin-top: 200px;
	}
</style>
