<script>
	import EndScreen from './End.svelte'

	import { createEventDispatcher } from 'svelte'
	const dispatch = createEventDispatcher()

	export let rounds

	const onEnd = () => {
		dispatch('nextscreen', {
			screen: EndScreen
		})
	}
</script>

<div class='container'>
	<h3>Score - 0:0</h3>
	<div class='board'>
		<div class='board-item'>1</div>
		<div class='board-item'>2</div>
		<div class='board-item'>3</div>
		<div class='board-item'>4</div>
		<div class='board-item'>5</div>
		<div class='board-item'>6</div>
		<div class='board-item'>7</div>
		<div class='board-item'>8</div>
		<div class='board-item'>9</div>
	</div>
</div>

<style>
	.container {
		margin: auto;
		text-align: center;
		margin-top: 8rem;
		max-width: 15rem;
		max-height: 15rem;
		background-color: coral;
	}

	.board {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		grid-gap: 3px;
	}

	.board-item {
		display: block;
		width: 100%;
		height: 100%;
		background-color: #ccc;
		text-align: center;
	}
</style>
