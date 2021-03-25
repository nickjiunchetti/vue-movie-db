<template>
	<div class="movie-detail">
		<h2>{{movie.Title}}</h2>
		<p>{{movie.Year}}</p>
		<img :src="movie.Poster" alt="Movie Poster" class="featured-img"/>
		<p>{{movie.Plot}}</p>
	</div>
</template>

<script>
	import {ref, onBeforeMount } from 'vue'
	import {useRoute} from 'vue-router'
	import env from '@/env.js'

export default {
	setup() {
		const movie = ref({})
		const route = useRoute()

		onBeforeMount(() => {
			fetch(`${env.url}?i=${route.params.id+env.apikey}&plot=full`)
				.then(response => response.json())
				.then(data => {
					movie.value = data
				})
		})

		return {
			movie
		}
	}
}
</script>

<style lang="scss">
	.movie-detail {
		padding: 16px;
		h2{
			color: #fff;
		}

		.feature-img {
			display: block;
			max-width: 200px;
			margin-bottom: 16px;
		}

		p {
			color: #fff;
			font-size: 18px;
			line-height: 1.4;
		}
	}



</style>