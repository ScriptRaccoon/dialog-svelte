# Dialog and Modal components in Svelte

This repository contains a reusable Svelte component (`Dialog.svelte`) for displaying customizable, accessible dialogs and modals. There is also a demonstration of various use cases (`App.svelte`).

https://dialog-svelte.netlify.app/

## Usage

Simple copy-paste the component `Dialog.svelte` into your Svelte project and adjust it as needed. Then import it and its `open_dialog` function.

```typescript
import Dialog, { open_dialog } from "./lib/Dialog.svelte"

open_dialog({
	confirm: { text: "Yes", action: () => delete_item(item) },
	cancel: { text: "No", action: () => {} },
	text: "Do you really want to delete the item?",
	modal: true,
})

function delete_item(item: Item) {
	// actually delete the item
}
```
