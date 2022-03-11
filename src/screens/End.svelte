<script>
	import StartScreen from './Start.svelte'

	import { createEventDispatcher } from 'svelte'
	const dispatch = createEventDispatcher()

	const onClick = () => {
		dispatch('nextscreen', {
			screen: StartScreen
		})
	}
</script>

<h1>End</h1>
<button on:click={onClick}>Restart</button>
