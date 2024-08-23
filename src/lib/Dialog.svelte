<script lang="ts">
	import type { Snippet } from 'svelte';
	import type { HTMLDialogAttributes } from 'svelte/elements';

	type Props = {
		// Variables
		isOpen?: boolean;
		closeOnOutsideClick?: boolean;
		children?: Snippet;

		// Events
		onopen?: EventListener;
		onclose?: EventListener;

		// Styles
		'--backdrop-color'?: string;
		'--transition-duration'?: string;
	} & HTMLDialogAttributes;

	// Variables
	let element: HTMLDialogElement;
	let {
		isOpen = $bindable(),
		closeOnOutsideClick = true,
		children,

		// Events
		onopen,
		onclose,

		...restProps
	}: Props = $props();

	// Effect for isOpen state to open and close the dialog
	$effect(() => {
		if (!element) return;

		if (isOpen) {
			element.showModal();
			const event = new Event('open');
			if (onopen) onopen(event);
		} else {
			element.close();
		}
	});

	// Add event listeners
	$effect(() => {
		if (!element) return;

		const closeHandler = (e: Event) => {
			isOpen = false;
			if (onclose) onclose(e);
		};

		const clickHandler = (event: MouseEvent) => {
			if (!closeOnOutsideClick) return;

			if (event.target === element) {
				isOpen = false;
			}
		};

		element.addEventListener('close', closeHandler);
		element.addEventListener('click', clickHandler);

		return () => {
			element.removeEventListener('close', closeHandler);
			element.removeEventListener('click', clickHandler);
		};
	});
</script>

<dialog bind:this={element} {...restProps}>
	{#if children}
		{@render children()}
	{/if}
</dialog>

<style>
	/* Rest default value */
	dialog {
		opacity: 0;
		border: unset;
		background: unset;
		max-width: unset;
		max-height: unset;
		padding: unset;

		/* Animation */
		transition: all var(--transition-duration, 0.3s) allow-discrete;
	}

	dialog:focus {
		outline: none;
	}

	dialog[open] {
		opacity: 1;
	}

	@starting-style {
		dialog[open] {
			opacity: 0;
		}
	}

	dialog::backdrop {
		background-color: rgb(0 0 0 / 0%);
		transition: all var(--transition-duration, 0.3s) allow-discrete;
	}

	dialog[open]::backdrop {
		background-color: var(--backdrop-color, rgba(0, 0, 0, 0.2));
	}

	@starting-style {
		dialog[open]::backdrop {
			background-color: rgb(0 0 0 / 0%);
		}
	}
</style>
