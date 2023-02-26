<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();
	export let text;
	export let href;
	export let children;

	function closeNavMenu() {
		dispatch('closeNavMenu');
	}
</script>

{#if !children}
	<a {href} class="text-zinc-200 text-xl py-2" on:click={closeNavMenu}>{text}</a>
{:else}
	<p class="text-zinc-200">Handling children...</p>
{/if}
