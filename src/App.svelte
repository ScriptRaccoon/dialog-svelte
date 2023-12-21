<script lang="ts">
	import { shuffle } from "./lib/utils"
	import { type Item } from "./lib/types"
	import Header from "./lib/Header.svelte"
	import Menu from "./lib/Menu.svelte"
	import Items from "./lib/Items.svelte"

	const AMOUNT = 12

	const original_items = Array.from({ length: AMOUNT }).map((_, i) => ({
		source: `https://unsplash.it/${300 + i}/200`,
		id: crypto.randomUUID(),
	}))

	let items: Item[] = original_items

	function confirm_delete_item(item: Item) {
		const confirm = window.confirm("Do you really want to delete the item?")
		if (confirm) delete_item(item)
	}

	function delete_item(item: Item) {
		items = items.filter((_item) => _item != item)
		if (items.length === 0) setTimeout(confirm_create_items, 500)
	}

	function open_shuffle_modal() {
		const confirm = window.confirm(
			"This will shuffle the items in a random order.",
		)
		if (confirm) shuffle_items()
	}

	function shuffle_items() {
		items = shuffle(items)
	}

	function confirm_create_items() {
		const confirm = window.confirm(
			"There are no items left. Do you want to create new items?",
		)
		if (confirm) items = original_items
	}

	function alert_rotate() {
		window.alert("This feature is not implemented yet")
	}
</script>

<Header />

<main>
	<Menu {open_shuffle_modal} {alert_rotate} />

	<Items {items} {confirm_delete_item} />
</main>
