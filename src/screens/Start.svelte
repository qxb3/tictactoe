<script>
	import GameScreen from './Game.svelte'

	import { createEventDispatcher } from 'svelte'
	const dispatch = createEventDispatcher()

	let rounds = 0
	let sendError = false

	const onStart = () => {
		if (rounds > 0) {
			sendError = false
			dispatch('nextscreen', {
				screen: GameScreen,
				args: {
					rounds
				}
			})
		} else {
			sendError = true
		}
	}
</script>

<div class='container'>
	<h1>TicTacToe</h1>
	<div>
		<p><strong>How many rounds:</strong></p>
		<input on:input={(event) => rounds = event.target.value} type='number' placeholder='10'/>
	</div>
	{#if sendError === true}
		<div class='error'>
			<p>Rounds needs to be higher than 0</p>
		</div>
	{/if}
	<button on:click={onStart}>Start</button>
</div>

<style>
	.container {
		text-align: center;
		padding-top: 5rem;
	}

	h1, button {
		margin: 3rem;
	}

	.error {
		display: 100%;
		background-color: orange;
		padding: 0.5rem;
	}
</style>
