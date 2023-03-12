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
			href: '/about',
			text: 'About'
		},
		{
			href: '/jupiter',
			text: 'Jupiter'
		},
		{
			href: '/student-loans',
			text: 'Student Loans'
		},
		{
			href: '/running',
			text: 'Running'
		}
	];
</script>

<body>
	<div class="stars-container bg-zinc-900 min-h-screen">
		<div class="stars" />
		<div class="stars" />
		<div class="stars" />
		<div class="stars" />
		<div class="stars" />
		<div class="stars" />
	</div>
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
			<h1>
				<a class="inline-block text-zinc-200 align-middle text-4xl" href="/">Collin Sinclair</a>
			</h1>
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

<style lang="scss">
	.stars-container,
	.stars {
		position: fixed;
		top: 0;
		right: 0;
		bottom: 0;
		left: 0;
		overflow: hidden;
		z-index: -1;
	}

	.stars {
		background-image: radial-gradient(
				2px 2px at 37px 138px,
				rgb(208, 208, 208),
				rgb(152, 163, 188),
				rgba(0, 0, 0, 0)
			),
			radial-gradient(
				2px 2px at 137px 223px,
				rgb(250, 255, 245),
				rgb(208, 180, 123),
				rgba(0, 0, 0, 0)
			),
			radial-gradient(
				2px 2px at 247px 15px,
				rgb(208, 208, 208),
				rgb(157, 177, 224),
				rgba(0, 0, 0, 0)
			),
			radial-gradient(
				2px 2px at 293px 36px,
				rgb(250, 255, 245),
				rgb(230, 207, 163),
				rgba(0, 0, 0, 0)
			),
			radial-gradient(1px 2px at 195px 160px, #ddd, rgba(0, 0, 0, 0));
		background-repeat: repeat;
		background-size: 300px 300px;
		opacity: 0;
		animation: zoom 10s infinite;

		&:nth-child(1) {
			background-position: 10% 90%;
			animation-delay: 0s;
		}

		&:nth-child(2) {
			background-position: 20% 50%;
			background-size: 270px 500px;
			animation-delay: 0.3s;
		}

		&:nth-child(3) {
			background-position: 40% -80%;
			animation-delay: 1.2s;
		}

		&:nth-child(4) {
			background-position: -20% -30%;
			transform: rotate(60deg);
			animation-delay: 2.5s;
		}

		&:nth-child(5) {
			background-image: radial-gradient(
					2px 2px at 37px 138px,
					rgb(208, 208, 208),
					rgb(152, 163, 188),
					rgba(0, 0, 0, 0)
				),
				radial-gradient(
					2px 2px at 137px 223px,
					rgb(250, 255, 245),
					rgb(208, 180, 123),
					rgba(0, 0, 0, 0)
				),
				radial-gradient(
					2px 2px at 247px 15px,
					rgb(208, 208, 208),
					rgb(157, 177, 224),
					rgba(0, 0, 0, 0)
				),
				radial-gradient(
					2px 2px at 293px 36px,
					rgb(250, 255, 245),
					rgb(230, 207, 163),
					rgba(0, 0, 0, 0)
				),
				radial-gradient(1px 2px at 195px 160px, #ddd, rgba(0, 0, 0, 0));
			background-position: 80% 30%;
			animation-delay: 4s;
		}

		&:nth-child(6) {
			background-position: 50% 20%;
			animation-delay: 6s;
		}
	}

	@keyframes zoom {
		0% {
			opacity: 0;
			transform: scale(0.5);
			transform: rotate(5deg);
			animation-timing-function: ease-in;
		}
		50% {
			opacity: 1;
		}
		100% {
			opacity: 0;
			transform: scale(2.2);
		}
	}

	@media (prefers-reduced-motion) {
		.stars {
			animation: none;
		}
	}
</style>
