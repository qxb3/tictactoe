<script>
	import StartScreen from './Start.svelte'

	import { createEventDispatcher } from 'svelte'
	const dispatch = createEventDispatcher()

	export let playerScore
	export let botScore

	const restart = () => {
		dispatch('nextscreen', {
			screen: StartScreen
		})
	}
</script>

<div class='container'>
	<h3>Your score: {playerScore}</h3>
	<h3>Bot score: {botScore}</h3>
	<h4>Play again?</h4>
	<button on:click={restart}>Restart</button>
</div>

<style>
	.container {
		text-align: center;
		width: 16rem;
		margin: 12rem auto auto auto;
	}

	h4 {
		margin-top: 6rem;
	}
</style>
