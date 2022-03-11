<script>
	import StartScreen from './screens/Start.svelte'

	let currentScreen = StartScreen
	const onNextScreen = (event) => {
		currentScreen = event.detail
	}
</script>

<svelte:component this={currentScreen} on:nextscreen={onNextScreen}/>

<style>
</style>
