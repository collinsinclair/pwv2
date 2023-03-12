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
	<h2>
		<a {href} class="text-zinc-200 hover:text-zinc-400 text-2xl my-2" on:click={closeNavMenu}
			>{text}</a
		>
	</h2>
{:else}
	<p class="text-zinc-200">Handling children...</p>
{/if}
