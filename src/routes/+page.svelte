<script lang="ts">
	import Placeholder from '$lib/Placeholder.svelte'
	import Section from '$lib/root/Section.svelte'
	import type { Snippet } from 'svelte'
	import { type IconSource } from 'svelte-hero-icons'
</script>

<svelte:head>
	<title>xylight.dev</title>
	<meta name="description" content="Xylight's portfolio" />
</svelte:head>

<div class="main">
	<header class="main-header">
		<div class="glow"></div>
		<div class="flex flex-col justify-end h-full space-y-2 text-xl gap-4 max-w-7xl w-full mx-auto">
			<nav class={['flex items-center flex-wrap justify-start px-5 sm:px-16']}>
				{#snippet link(href: string, label: string, index: number = 0)}
					<a
						{href}
						class={[
							'font-medium text-base hover:underline',
							'px-3 lg:px-4 py-2 transition-colors inline-flex flex-row items-center gap-2'
						]}
					>
						{label}
					</a>
				{/snippet}

				{@render link('/', 'Home')}
				{@render link('/#projects', 'Projects')}
				{@render link('/posts', 'Posts')}
			</nav>
			<h1
				class={[
					'tracking-tighter text-7xl sm:text-8xl lg:text-9xl font-display px-8 sm:px-16 w-max flex gap-4 '
				]}
			>
				<span
					class="dark:bg-gradient-to-b dark:text-transparent bg-clip-text dark:from-zinc-50 dark:to-red-200 pb-5 pr-5"
				>
					xylight.dev
				</span>
			</h1>
		</div>
	</header>

	{#snippet social(href: string, label: string)}
		<a {href} class="inline text-indigo-600 dark:text-indigo-400 hover:underline decoration-2">
			{label}
		</a>
	{/snippet}

	<Section>
		<heading>
			<div
				class="text-2xl sm:text-2xl text-zinc-500 dark:text-zinc-400 max-w-3xl leading-[1.5] space-y-6 text-left font-medium tracking-tight"
			>
				<p>
					<span class="text-zinc-900 dark:text-zinc-50">
						I am a hobbyist developer, UX designer, and sysadmin.
					</span>
					I try to create applications that are helpful, and convenient.
				</p>
				<p>
					{@render social('https://matrix.to/#/@xylight:chat.phtn.app', 'Matrix')}, {@render social(
						'https://github.com/Xyphyn',
						'GitHub'
					)},
					{@render social('https://lemdro.id/u/Xylight', 'Lemmy')}, {@render social(
						'https://mas.to/@Xylight',
						'Mastodon'
					)}.
				</p>
			</div>
		</heading>
	</Section>
	<Section>
		<h2
			id="projects"
			class="font-display mb-12 italic text-5xl sm:text-6xl tracking-tight text-center"
		>
			Projects
		</h2>
		<div class="flex flex-row flex-wrap sm:px-16 gap-x-8 gap-y-16 w-full text-left">
			{#snippet project(
				number: number,
				name: string,
				description: string,
				icon?: IconSource,
				url?: string,
				img?: Snippet
			)}
				<svelte:element
					this={url ? 'a' : 'article'}
					href={url}
					class={[
						'flex flex-col gap-1 border rounded-3xl border-zinc-200 dark:border-zinc-800 p-6 w-full min-w-[12rem]',
						'hover:bg-indigo-500/2 transition-colors group  relative overflow-hidden flex-1 first:flex-2'
					]}
				>
					{#if img}
						<div
							class="h-48 overflow-hidden grid place-items-center rounded-2xl *:scale-150 -m-7 mask-b-from-0%"
						>
							{@render img()}
						</div>
					{/if}
					<div class={['flex items-center gap-2']}>
						<h3 class={['font-display text-2xl font-medium tracking-tight']}>
							{name}
						</h3>
					</div>
					<p class="max-w-md text-zinc-600 dark:text-zinc-400">
						{description}
					</p>
				</svelte:element>
			{/snippet}

			{#snippet photonImg()}
				<div class="contents dark:hidden">
					<enhanced:img
						src="./photon.png?w=640,320"
						sizes="(min-width:1280px) 640px, (min-width:720px) 320px"
						alt="A screenshot of the interface of Photon"
						class="object-cover object-top w-full"
					/>
				</div>
				<div class="hidden dark:contents">
					<enhanced:img
						src="./photon-dark.png?w=640,320"
						sizes="(min-width:1280px) 640px, (min-width:720px) 320px"
						alt="A screenshot of the interface of Photon"
						class="object-cover object-top w-full"
					/>
				</div>
			{/snippet}
			{#snippet placeholder()}
				<div class="scale-200 origin-center h-full overflow-hidden">
					<Placeholder seed="red" />
				</div>
			{/snippet}
			{@render project(
				0,
				'Photon',
				`A fully-featured, well designed, and mature Svelte based web client for the fediverse.`,
				undefined,
				'https://use.phtn.app',
				photonImg
			)}
			{@render project(
				1,
				'Websites like this',
				`Svelte is my typical framework of choice.`,
				undefined,
				'https://github.com/Xyphyn/xyphyn.github.io',
				placeholder
			)}
		</div>
		<p class="tracking-tight text-xl text-zinc-600 dark:text-zinc-400 max-w-3xl px-8 sm:px-24">
			If you'd like to support my work, especially on Photon, you can donate at {@render social(
				'https://buymeacoffee.com/xylight',
				'Buy me a Coffee'
			)}.
		</p>
	</Section>
</div>

<style>
	@reference '../app.css';

	.main {
		z-index: 0;
		gap: calc(var(--spacing) * 8);
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}

	.main-header {
		border-bottom: 1px solid var(--color-zinc-200);
		overflow: hidden;
		min-height: calc(var(--spacing) * 56);

		padding-top: calc(var(--spacing) * 6);
		padding-bottom: calc(var(--spacing) * 6);

		position: relative;
		z-index: 0;
		width: 100%;
		display: flex;
		flex-direction: column;
		justify-content: end;

		@variant sm {
			min-height: calc(var(--spacing) * 96);
			padding-top: calc(var(--spacing) * 16);
			padding-bottom: calc(var(--spacing) * 16);
		}

		@variant lg {
			min-height: 36rem;
		}

		@variant dark {
			border-color: var(--color-zinc-800);
		}
	}

	@keyframes brighten {
		from {
			opacity: 0.5;
		}
		to {
			opacity: 1;
		}
	}

	.glow {
		--max-opacity: 0.7;
		@media (prefers-color-scheme: dark) {
			--max-opacity: 0.4;
		}

		animation: brighten ease-out 1s forwards;

		position: absolute;
		width: 150%;
		top: 0;
		height: 48rem;
		max-width: 100%;
		z-index: -1;
		overflow: hidden;
		background: radial-gradient(
			ellipse at top center in oklch,
			oklch(75% 0.083 55.934 / var(--max-opacity)),
			oklch(65.6% 0.141 354.308 / calc(var(--max-opacity) / 2)),
			oklch(67.3% 0.182 276.935 / 0) 70%,
			transparent
		);
		background-position: 50% 0%;
		background-size: 50rem 30rem;
		background-repeat: no-repeat;
		pointer-events: none;

		@variant sm {
			width: 100%;
			background-size: 50rem 30rem;
		}
		@variant lg {
			background-size: 125rem 48rem;
		}
	}
</style>
