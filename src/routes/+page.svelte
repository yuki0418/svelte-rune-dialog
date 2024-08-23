<script lang="ts">
	import { Dialog } from '$lib/index.js';

	let isOpen = $state(false);

	const toggleDialog = () => {
		isOpen = !isOpen;
	};

	const closeDialog = () => {
		isOpen = false;
	};
</script>

{#snippet button(onclick: () => void, text?: string)}
	<button {onclick}>
		{#if text}
			{text}
		{:else}
			Click me
		{/if}
	</button>

	<style>
		button {
			padding: 10px 20px;
			border: none;
			border-radius: 5px;
			background-color: #007bff;
			color: white;
			cursor: pointer;
			border-radius: var(--radius);
		}
	</style>
{/snippet}

{#snippet container()}
	<div class="container">
		<p>Dialog content</p>
		<p>You can close the dialog by ESC as well</p>
		<div>
			{@render button(closeDialog, 'Close')}
		</div>
	</div>

	<style>
		.container {
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: center;
			min-width: 500px;
			min-height: 300px;
			background-color: white;
			border-radius: var(--radius);
		}

		.container p {
			margin: 0;
			padding: 10px;
		}

		.container div {
			margin-top: 20px;
		}
	</style>
{/snippet}

<div class="main-container">
	<h1>Svelte Rune Dialog Example</h1>

	<button onclick={toggleDialog}>{isOpen ? 'Close' : 'Open'} dialog</button>
	<Dialog bind:isOpen>
		{@render container()}
	</Dialog>
</div>

<style>
	@import url('https://fonts.googleapis.com/css2?family=M+PLUS+1p:wght@100;300;400;500;700;800;900&family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap');

	:root {
		box-sizing: border-box;

		--radius: 3px;
	}

	.main-container {
		font-family: 'Roboto', sans-serif;
		display: flex;
		flex-direction: column;
		justify-content: start;
		align-items: center;
		min-height: 100vh;
		padding-top: 30rem;
	}
</style>
