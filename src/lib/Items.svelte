<script lang="ts">
	import { faTrashAlt } from "@fortawesome/free-solid-svg-icons"
	import Fa from "svelte-fa"
	import { flip } from "svelte/animate"
	import { fade } from "svelte/transition"
	import type { Item } from "../utils"

	export let confirm_delete_item: (item: Item) => void
	export let items: Item[] = []
</script>

<ul class="items">
	{#each items as item (item.id)}
		<li
			class="item"
			transition:fade={{ duration: 200 }}
			animate:flip={{ duration: 200 }}
		>
			<div class="img-wrapper">
				<img src={item.source} alt="random resource from unsplash" />
			</div>
			<button on:click={() => confirm_delete_item(item)} aria-label="delete">
				<Fa icon={faTrashAlt} />
			</button>
		</li>
	{/each}
</ul>

<style>
	.item {
		position: relative;
	}

	.item button {
		position: absolute;
		top: 0.5rem;
		right: 0.5rem;
		color: white;
		background-color: #0004;
		padding: 0.5rem;
		aspect-ratio: 1/1;
		border-radius: 50%;
		display: flex;
		align-items: center;
		transition: background-color 100ms;
	}

	.item button:focus-visible,
	.item button:hover {
		background-color: #000a;
	}

	.img-wrapper {
		width: 300px;
		height: 200px;
		overflow: hidden;
		margin-bottom: 0.25rem;
		border-radius: 0.75rem;
		border-top-right-radius: 0rem;
	}

	.items {
		width: min(95vw, 80rem);
		margin-inline: auto;
		display: flex;
		flex-wrap: wrap;
		gap: 1rem;
	}

	img {
		display: block;
	}
</style>
