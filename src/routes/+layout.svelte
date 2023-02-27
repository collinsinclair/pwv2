<script lang="ts">
	import '../app.css';
	import NavItem from './NavItem.svelte';
	import profilePicture from '$lib/img/profile-picture.jpeg';
	import { fade } from 'svelte/transition';

	let navMenuOpen = false;
	const navItems = [
		{
			href: '/',
			text: 'Home'
		},
		{
			href: '/jupiter',
			text: 'Jupiter'
		},
		{
			href: '/student-loans',
			text: 'Student Loans'
		}
	];
</script>

<body class="bg-zinc-900 min-h-screen">
	<nav>
		<div class="px-3 py-3 flex items-center flex justify-between">
			<button
				on:click={() => (navMenuOpen = !navMenuOpen)}
				class="inline-block cursor-pointer align-middle"
				aria-label="Menu Button"
			>
				{#if !navMenuOpen}
					<svg
						xmlns="http://www.w3.org/2000/svg"
						fill="none"
						viewBox="0 0 24 24"
						stroke-width="1.5"
						stroke="#e4e4e7"
						class="w-10 h-10"
					>
						<path
							stroke-linecap="round"
							stroke-linejoin="round"
							d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5"
						/>
					</svg>
				{:else}
					<svg
						xmlns="http://www.w3.org/2000/svg"
						fill="none"
						viewBox="0 0 24 24"
						stroke-width="1.5"
						stroke="#e4e4e4"
						class="w-10 h-10"
					>
						<path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
					</svg>
				{/if}
			</button>
			<a class="inline-block text-zinc-200 align-middle text-4xl" href="/">Collin Sinclair</a>
			<img
				src={profilePicture}
				class="h-10 w-10 rounded-full"
				alt="A white man wearing glasses, smiling."
			/>
		</div>
		{#if navMenuOpen}
			<div class="flex flex-col items-center" transition:fade>
				{#each navItems as navItem}
					<NavItem
						href={navItem.href}
						text={navItem.text}
						children={navItem.children}
						on:closeNavMenu={() => (navMenuOpen = false)}
					/>
				{/each}
			</div>
		{/if}
	</nav>
	<slot />
</body>
