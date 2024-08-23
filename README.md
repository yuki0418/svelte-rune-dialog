# Svelte Rune Dialog
Svelte Rune Dialog is a simple dialog component for Svelte 5.

Use `<dialog>` element so dialog content will be rendered at `#top-layer`. If you want to know more about `<dialog>` element, please refer to [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/dialog).

> [!IMPORTANT]  
> Svelte Rune Dialog uses `@starting-style` for animations. Some browsers may not support `@starting-style`. You can check if your browser supports `@starting-style` by visiting [Can I use](https://caniuse.com/mdn-css_at-rules_starting-style).

# How to use
You can use this component easily as an example below.

```svelte
<script lang="ts">
	import { Dialog } from '$lib/index.js';

	let isOpen = $state(false);

	const toggleDialog = () => {
		isOpen = !isOpen;
	};

	const closeDialog = () => {
		isOpen = false;
	}
</script>

<h1>Svelte Rune Dialog Example</h1>
<button onclick={toggleDialog}>{isOpen ? 'Close' : 'Open'} dialog</button>

<Dialog bind:isOpen --backdrop-color="rgba(0, 0, 0, 0.8)">
  <div>
    <h2>Dialog Title</h2>
    <p>Dialog Content</p>
    <button onclick={closeDialog}>Close</button>
  </div>
</Dialog>
```

# Properties
| Property | Type | Description | Default |
| --- | --- | --- | --- |
| isOpen | boolean? | Dialog open or close state | false |
| closeOnOutsideClick | boolean? | Close dialog when overlay clicked | true |

# Events
| Event | Type | Description |
| --- | --- | --- |
| onopen | EventListener? | Fired when dialog closed |
| onclose | EventListener? | Fired when dialog closed |

# Style properties
| Property | Type | Description | Default |
| --- | --- | --- | --- |
| --backdrop-color | String? | Backdrop color | rgba(0, 0, 0, 0.2) |
| --transition-duration | String? | Transition duration | 0.3s |

# Demo
You can see the demo by following steps below.
1. Clone this repository.
2. Run `npm install` to install dependencies.
3. Run `npm run dev` or `npm run dev -- --open` to start the development server.
4. Open `http://localhost:5173` in your browser.

If you use `yarn` then
1. Clone this repository.
2. Run `yarn install` to install dependencies.
3. Run `yarn dev` or `yarn dev --open` to start the development server.
4. Open `http://localhost:5173` in your browser.
