<script>
	import { flip } from 'svelte/motion';
	class Block {
		constructor(width, height, x, y) {
			this.width = width;
			this.height = height;
			this.x = x;
			this.y = y;
		}
	}
	let grid = $state({
		a: new Block(1, 1, 1, 1),
		b: new Block(1, 2, 2, 1),
		c: new Block(2, 1, 3, 1),
		d: new Block(1, 1, 5, 1),
		e: new Block(1, 2, 1, 2),
		f: new Block(2, 2, 3, 2),
		g: new Block(1, 2, 5, 2),
		h: new Block(1, 1, 1, 4),
		i: new Block(2, 1, 3, 4),
		j: new Block(1, 1, 5, 4),
		k: new Block(2, 1, 1, 5),
		l: new Block(2, 1, 3, 5),
		m: new Block(1, 1, 5, 5)
	});
	let listGrid = $derived(Object.values(grid));
	// let grid = $state([
	// 'abccd',
	// 'ebffg',
	// 'e-ffg',
	// 'h-iij',
	// 'kkllm']);
</script>

<main>
	<h1>Door Puzzle</h1>
	<div id="container">
		{#each listGrid as block (block)}
			<div
				class="block"
				style="--width:{block.width}; --height:{block.height}; --xPos: {block.x}; --yPos: {block.y}"
			></div>
		{/each}
	</div>
</main>

<style>
	h1 {
		margin-top: 0;
		width: max-content;
		background-color: grey;
		padding: 0.25em;
		margin: 0 auto;
		border: 2px solid black;
		border-radius: 0.5em;
	}
	#container {
		width: 25em;
		height: 25em;
		box-sizing: content-box;
		border: 2px solid darkgrey;
		margin: 5em auto 0 auto;
		background: black;
		display: grid;
		grid-template: repeat(5, 5em) / repeat(5, 5em);
	}
	.block {
		border: 2px solid transparent;
		width: calc(var(--width) * 5em);
		height: calc(var(--height) * 5em);
		grid-column: var(--xPos) / span var(--width);
		grid-row: var(--yPos) / span var(--height);
		background-color: grey;
		background-clip: content-box;
	}
</style>
