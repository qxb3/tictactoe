<script>
	import EndScreen from './End.svelte'

	import { createEventDispatcher } from 'svelte'
	const dispatch = createEventDispatcher()

	export let rounds
	let playerScore = 0
	let botScore = 0

	let grid = [
		'~', '~', '~',
		'~', '~', '~',
		'~', '~', '~',
	]

	const checkWinner = (char) => {
		if (
			//Check horizontally
			grid[0] === char && grid[1] === char && grid[2] === char ||
			grid[3] === char && grid[4] === char && grid[5] === char ||
			grid[6] === char && grid[7] === char && grid[8] === char ||
			//Check vertically
			grid[0] === char && grid[3] === char && grid[6] === char ||
			grid[1] === char && grid[4] === char && grid[7] === char ||
			grid[2] === char && grid[5] === char && grid[8] === char ||
			//Check diagonally
			grid[0] === char && grid[4] === char && grid[8] === char ||
			grid[6] === char && grid[4] === char && grid[2] === char
		) return true

		return false
	}

	const clearBoard = () => {
		grid = [
			'~', '~', '~',
			'~', '~', '~',
			'~', '~', '~',
		]
	}

	const playersTurn = (index) => {
		if (grid[index] === 'O') return false
		if (grid[index] === '~') {
			grid[index] = 'X'
			return true
		}
	}

	const botsTurn = () => {
		const random = Math.floor(Math.random() * 9)
		if (grid[random] === '~') {
			grid[random] = 'O'
		} else if (!grid.every(cell => cell !== '~')) {
			botsTurn()
		}
	}

	const onCellClick = (index) => {
		const turn = playersTurn(index)
		if (turn) botsTurn()

		//Check winner
		if (checkWinner('X')) {
			rounds--
			playerScore++
			clearBoard()
		}
		if (checkWinner('O')) {
			rounds--
			botScore++
			clearBoard()
		}

		//Check if the grid is full
		if (grid.every(cell => cell !== '~')) {
			rounds--
			clearBoard()
		}

		if (rounds <= 0) {
			dispatch('nextscreen', {
				screen: EndScreen,
				args: {
					playerScore,
					botScore
				}
			})
		}
	}
</script>

<h3 class='rounds'>Rounds left: {rounds}</h3>

<div class='main'>
	<h3>Score: {playerScore} - {botScore}</h3>
	<div class='board'>
		{#each grid as cell, index}
			<div class='cell' on:click={() => onCellClick(index)}>{cell}</div>
		{/each}
	</div>
</div>

<style>
	.main {
		text-align: center;
		width: 18rem;
		height: 15rem;
		margin: 6rem auto auto auto;
	}

	h3 {
		margin-bottom: 3rem;
	}

	.board {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		grid-template-rows: repeat(3, 70px);
		grid-gap: 2px;
		margin-top: 1rem;
	}

	.rounds {
		display: fixed;
		top: 0;
		margin: 1rem;
	}

	.cell {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		background-color: #fff;
		box-shadow: 0 2px 4px 0 rgba(0,0,0,0.2);
		transition: 0.3s;
	}

	.cell:hover {
		background-color: #ccc;
	}
</style>
