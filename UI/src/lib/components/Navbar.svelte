<script>
	import Button from './Button.svelte';
	import Burger from './icons/Burger.svelte';
	import X from './icons/X.svelte';
	import { fly } from 'svelte/transition';
	import { clickOutside } from '../clickOutside';
	import ConnectButton from './ConnectButton.svelte';

	export let dashboard = false;
	let open = false;
</script>

<div class="wrap" use:clickOutside={() => (open = false)}>
	<div class="navbar">
		<a
			href="#menu"
			on:click={(e) => {
				e.preventDefault();
				open = true;
			}}
		>
			<Burger />
		</a>
		<div class="logo" class:dashboard>
			<a href="/">
				<img src="/images/logo.png" alt="InpulseX logo" />
			</a>
		</div>
		<div class="buttons" class:dashboard>
			{#if dashboard}
				<ConnectButton />
			{:else}
				<Button href="/dashboard">Dashboard</Button>
			{/if}
		</div>
	</div>

	{#if open}
		<div class="sidebar" transition:fly={{ x: -200, duration: 200 }}>
			<a
				href="#menu"
				on:click={(e) => {
					e.preventDefault();
					open = false;
				}}
			>
				<X />
			</a>
			<a href="/#about">About</a>
			<a href="/#pillars">Pillars</a>
			<a href="/#game">Starseed Awakening</a>
			<a href="/#characters">NFT Custom Characters</a>
			<a href="/#team">Team</a>
			<a href="/#tokenomics">Tokenomics</a>
			<a href="/#spacemap">SpaceMap</a>
			<a href="/#certificates">Certificates</a>
			<a target="_blank" rel="noreferrer" href="https://linktr.ee/inpulsex_official">
				Social Channels
			</a>
			<a href="/dashboard">Dashboard</a>
		</div>
	{/if}
</div>

<style>
	.navbar {
		display: grid;
		grid-template-columns: 1fr 1fr 1fr;
		gap: 2em;
		position: fixed;
		top: 0;
		z-index: 100;
		background: rgba(0, 0, 0, 0.4);
		backdrop-filter: blur(16px);
		-webkit-backdrop-filter: blur(16px);
		align-items: center;
		width: 100%;
		padding: 1em 4em;
		box-sizing: border-box;
	}
	.logo {
		text-align: center;
	}
	.buttons {
		display: flex;
		justify-content: end;
	}
	.sidebar {
		position: fixed;
		left: 0;
		top: 0;
		z-index: 100;
		width: 320px;
		height: 100%;
		background: rgba(0, 0, 0, 0.4);
		backdrop-filter: blur(16px);
		-webkit-backdrop-filter: blur(16px);
		box-sizing: border-box;
		padding: 4em;
		display: flex;
		gap: 2em;
		flex-direction: column;
		padding-top: 1.5em;
	}
	a {
		color: #fff;
		text-decoration: none;
	}
	a:hover {
		transition: cubic-bezier(0.23, 1, 0.32, 1) all 0.4s;
		color: var(--primary-pink);
	}
	img {
		height: 2em;
	}
	@media only screen and (max-width: 600px) {
		.navbar {
			padding: 0.5em 1em;
			grid-template-columns: 1fr 1fr 6fr;
		}
		.sidebar {
			padding: 1em 2em;
		}
		.logo.dashboard {
			visibility: hidden;
			opacity: 0;
		}
		img {
			height: 1.2em;
			position: absolute;
			top: 50%;
			left: 50%;
			transform: translate(-50%, -50%);
		}
		.buttons:not(.dashboard) {
			display: none;
		}
	}
</style>
