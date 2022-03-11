<script>
	import EndScreen from './End.svelte'

	import { createEventDispatcher } from 'svelte'
	const dispatch = createEventDispatcher()

	const onClick = () => {
		dispatch('nextscreen', EndScreen)
	}
</script>

<h1>Game</h1>
<button on:click={onClick}>End</button>
