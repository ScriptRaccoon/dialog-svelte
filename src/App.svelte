<script lang="ts">
	import Dialog, { open_dialog } from "./lib/Dialog.svelte"
	import { shuffle } from "./lib/utils"
	import type { Item } from "./lib/types"
	import Header from "./lib/Header.svelte"
	import Menu from "./lib/Menu.svelte"
	import Items from "./lib/Items.svelte"

	const AMOUNT = 12

	const original_items = Array.from({ length: AMOUNT }).map((_, i) => ({
		source: `https://unsplash.it/${300 + i}/200`,
		id: crypto.randomUUID(),
	}))

	let items: Item[] = original_items

	function confirm_delete_item(item: Item): void {
		open_dialog({
			confirm: { text: "Yes", action: () => delete_item(item) },
			cancel: { text: "No", action: () => {} },
			text: "Do you really want to delete the item?",
			modal: true,
		})
	}

	function delete_item(item: Item): void {
		items = items.filter((_item) => _item != item)
		if (items.length === 0) setTimeout(confirm_create_items, 500)
	}

	function open_shuffle_modal(): void {
		open_dialog({
			confirm: { text: "Ok", action: shuffle_items },
			text: "This will shuffle the items in a random order.",
			modal: true,
		})
	}

	function shuffle_items(): void {
		items = shuffle(items)
	}

	function confirm_create_items(): void {
		open_dialog({
			confirm: { text: "Sure", action: () => (items = original_items) },
			cancel: { text: "No thanks", action: () => {} },
			text: "There are no items left. Do you want to create new items?",
		})
	}

	function alert_rotate(): void {
		open_dialog({
			confirm: { text: "Ok", action: () => {} },
			cancel: null,
			text: "This feature is not implemented yet",
		})
	}
</script>

<Header />

<main>
	<Menu {open_shuffle_modal} {alert_rotate} />

	<Items {items} {confirm_delete_item} />
</main>

<Dialog />
