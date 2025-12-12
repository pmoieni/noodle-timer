<script lang="ts">
	let { showModal = $bindable(), children } = $props();

	let dialog: HTMLDialogElement | null = $state(null);

	$effect(() => {
		if (dialog && showModal) dialog.showModal();
	});
</script>

<dialog
	bind:this={dialog}
	onclose={() => (showModal = false)}
	onclick={(e) => {
		if (dialog && e.target === dialog) dialog.close();
	}}
	open={false}
>
	<div>
		{@render children?.()}
	</div>
</dialog>

<style>
	dialog {
		border-radius: 0.5rem;
		margin: 0;
		left: 50%;
		top: 50%;
		transform: translate(-50%, -50%);
	}
</style>
