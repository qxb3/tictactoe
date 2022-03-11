<script>
	import StartScreen from './screens/Start.svelte'

	let currentScreen = StartScreen
	let args = {}

	const onNextScreen = (event) => {
		const { detail } = event

		currentScreen = detail.screen
		args = detail.args
	}
</script>

<svelte:component this={currentScreen} on:nextscreen={onNextScreen} {...args}/>
