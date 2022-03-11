<script>
	import GameScreen from './Game.svelte'

	import { createEventDispatcher } from 'svelte'
	const dispatch = createEventDispatcher()

	const onClick = () => {
		dispatch('nextscreen', GameScreen)
	}
</script>

<h1>Start</h1>
<button on:click={onClick}>Game</button>
