<script lang="ts">
	export let open_shuffle_modal: () => void
	export let alert_rotate: () => void
</script>

<menu class="actions">
	<button class="button" on:click={open_shuffle_modal}>Shuffle</button>
	<button class="button" on:click={alert_rotate}>Rotate</button>
</menu>

<style>
	.actions {
		display: flex;
		justify-content: center;
		gap: 0.5rem;
		margin-bottom: 2rem;
	}
</style>
