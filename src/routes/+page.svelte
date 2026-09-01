<script lang="ts">
	import { format } from 'date-fns';
	import { onMount } from 'svelte';

	let now = new Date();

	let testFormat = 'yyyy-MM-dd HH:mm:ss';

	let testFormatDateString = format(new Date(), testFormat);
	let copyMessage = '';

	onMount(() => {
		const timer = window.setInterval(() => {
			now = new Date();

			try {
				testFormatDateString = format(now, testFormat);
			} catch (error) {
				console.error(error);
				testFormatDateString = 'Invalid format';
			}
		}, 500);

		return () => window.clearInterval(timer);
	});

	async function copy(value: string, label: string) {
		try {
			await navigator.clipboard.writeText(value);
			copyMessage = `${label} copied`;
		} catch {
			copyMessage = 'Copy unavailable';
		}
	}

	const formatStrings = [
		'Pp',
		'PPpp',
		'PP',
		'PPP',
		"PP 'at' p",
		'MM/dd/y hh:mm a',
		"iii M/d 'at' p",
		'yyyy-MM-dd HH:mm:ss',
		'MM/dd/yyyy',
		'yyyy-MM-dd',
		'yyyy/MM/dd',
		'MMMM yyyy',
		'MMM d',
		'MMMM d',
		'eeee MM/dd/yyyy',
		'E MMM do',
		"MMMM d 'at' p",
		'MMMM d, yyyy',
		'eee',
		'eeee',
		'h:mm a'
	];
</script>

<svelte:head>
	<title>date-fns format helper</title>
	<meta name="theme-color" content="#102f2b" />
	<meta name="color-scheme" content="light only" />
	<meta
		name="description"
		content="A simple tool to help keep track of commonly used date formats. The tool is also helpful to test custom date formats."
	/>

	<meta property="og:image" content="https://date-fns.michaelbonner.dev/og-image.jpg" />
	<meta property="og:type" content="website" />
	<meta property="og:url" content="https://date-fns.michaelbonner.dev/" />
	<meta property="og:title" content="date-fns format helper" />

	<meta name="twitter:card" content="summary_large_image" />

	<link rel="canonical" href="https://date-fns.michaelbonner.dev/" />
</svelte:head>

<main class="isolate">
	<header class="border-b border-white/10 bg-[#102f2b] text-[#f7f5ef]">
		<div class="mx-auto flex max-w-7xl items-center justify-between gap-6 px-5 py-5 sm:px-8">
			<a href="/" aria-label="Homepage" class="font-semibold tracking-tight">date-fns / format</a>
			<a
				href="https://date-fns.org/docs/format"
				class="text-base/7 font-medium text-emerald-100 underline decoration-emerald-300/50 underline-offset-4 sm:text-sm/6"
				>Format documentation</a
			>
		</div>
	</header>

	<section class="border-b border-[#1c2528]/10 py-12 sm:py-16">
		<div class="mx-auto grid max-w-7xl gap-10 px-5 sm:px-8 lg:grid-cols-[21fr_19fr] lg:gap-16">
			<div class="grid content-start gap-6">
				<p class="font-mono text-base/7 text-emerald-800 sm:text-sm/6">LIVE FORMAT WORKBENCH</p>
				<h1
					class="max-w-[16ch] text-5xl font-semibold tracking-tight text-balance text-[#1c2528] sm:text-6xl"
				>
					Make dates say exactly what you mean.
				</h1>
				<p class="max-w-[52ch] text-lg/8 text-pretty text-[#526064] sm:text-base/7">
					A small, fast reference for experimenting with <code class="font-mono text-[#102f2b]"
						>date-fns</code
					>
					format tokens against the current time.
				</p>
			</div>

			<div class="border-l-4 border-emerald-600 bg-[#e7efe9] p-6 sm:p-8">
				<p class="font-mono text-base/7 text-emerald-900 sm:text-sm/6">YOUR REFERENCE TIME</p>
				<p
					class="mt-5 font-mono text-3xl font-medium tracking-tight tabular-nums text-[#102f2b] sm:text-4xl"
				>
					{now.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit', second: '2-digit' })}
				</p>
				<p class="mt-2 text-base/7 text-[#526064] sm:text-sm/6">
					{now.toLocaleDateString([], {
						weekday: 'long',
						month: 'long',
						day: 'numeric',
						year: 'numeric'
					})}
				</p>
			</div>
		</div>
	</section>

	<section class="py-12 sm:py-16">
		<div class="mx-auto grid max-w-7xl gap-10 px-5 sm:px-8 lg:grid-cols-[21fr_19fr] lg:gap-16">
			<div class="grid content-start gap-6">
				<div class="grid gap-3">
					<p class="font-mono text-base/7 text-emerald-800 sm:text-sm/6">01 / TRY A FORMAT</p>
					<h2
						class="max-w-[20ch] text-3xl font-semibold tracking-tight text-balance text-[#1c2528] sm:text-4xl"
					>
						Test any token string.
					</h2>
				</div>

				<label
					for="format-string"
					class="grid gap-3 text-base/7 font-medium text-[#1c2528] sm:text-sm/6"
				>
					Format string
					<input
						id="format-string"
						name="format-string"
						autocapitalize="off"
						autocomplete="off"
						autocorrect="off"
						bind:value={testFormat}
						class="w-full rounded-lg bg-white px-4 py-3 font-mono text-base/7 text-[#102f2b] ring-1 ring-[#1c2528]/15 outline-2 -outline-offset-1 outline-emerald-700 placeholder:text-[#778286] focus:ring-emerald-700 sm:text-sm/6"
						placeholder="yyyy-MM-dd HH:mm:ss"
						spellcheck="false"
						type="text"
					/>
				</label>
				<p class="text-base/7 text-pretty text-[#526064] sm:text-sm/6">
					Use quotes for literal text. Need a token refresher? Read the
					<a
						href="https://date-fns.org/docs/format"
						class="font-medium text-emerald-800 underline decoration-emerald-600/50 underline-offset-4"
						>official docs</a
					>.
				</p>
			</div>

			<div class="self-end border-y border-[#1c2528]/10 py-6 sm:py-8">
				<p class="font-mono text-base/7 text-emerald-800 sm:text-sm/6">OUTPUT</p>
				<p
					class="mt-4 break-words font-mono text-2xl font-medium tracking-tight tabular-nums text-[#102f2b] sm:text-3xl"
				>
					{testFormatDateString}
				</p>
				<div class="mt-6 flex flex-wrap items-center gap-4">
					<button
						type="button"
						onclick={() => copy(testFormatDateString, 'Result')}
						class="rounded-md bg-emerald-700 px-3 py-2 text-base/6 font-medium text-white ring-1 ring-emerald-700 focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-emerald-700 sm:text-sm/5"
					>
						Copy result
					</button>
					<p aria-live="polite" class="text-base/7 text-[#526064] sm:text-sm/6">{copyMessage}</p>
				</div>
			</div>
		</div>
	</section>

	<section class="border-t border-[#1c2528]/10 py-12 sm:py-16">
		<div class="mx-auto max-w-7xl px-5 sm:px-8">
			<div class="grid gap-3">
				<p class="font-mono text-base/7 text-emerald-800 sm:text-sm/6">02 / STARTING POINTS</p>
				<h2
					class="max-w-[24ch] text-3xl font-semibold tracking-tight text-balance text-[#1c2528] sm:text-4xl"
				>
					Useful formats, live and ready to copy.
				</h2>
			</div>

			<div class="mt-8 overflow-hidden rounded-xl border border-[#1c2528]/10 bg-white">
				<div
					class="grid grid-cols-[minmax(0,1fr)_auto] gap-4 border-b border-[#1c2528]/10 bg-[#eef1eb] px-5 py-3 font-mono text-base/7 text-[#526064] sm:grid-cols-[11rem_minmax(0,1fr)_auto] sm:px-6 sm:text-sm/6"
				>
					<span>FORMAT</span><span class="hidden sm:inline">EXAMPLE</span><span> </span>
				</div>
				<div>
					{#each formatStrings as formatString (formatString)}
						<div
							class="grid grid-cols-[minmax(0,1fr)_auto] items-center gap-4 border-b border-[#1c2528]/10 px-5 py-4 last:border-b-0 sm:grid-cols-[11rem_minmax(0,1fr)_auto] sm:px-6"
						>
							<code
								class="min-w-0 break-words font-mono text-base/7 font-medium text-[#102f2b] sm:text-sm/6"
								>{formatString}</code
							>
							<p
								class="hidden min-w-0 break-words text-base/7 text-[#526064] sm:block sm:text-sm/6"
							>
								{format(now, formatString)}
							</p>
							<button
								type="button"
								onclick={() => copy(formatString, 'Format')}
								class="rounded-md px-3 py-2 text-base/6 font-medium text-emerald-800 ring-1 ring-emerald-800/25 focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-emerald-700 sm:text-sm/5"
							>
								Copy
							</button>
						</div>
					{/each}
				</div>
			</div>
		</div>
	</section>

	<footer class="border-t border-[#1c2528]/10 py-8">
		<div
			class="mx-auto flex max-w-7xl flex-col gap-2 px-5 text-base/7 text-[#526064] sm:flex-row sm:items-center sm:justify-between sm:px-8 sm:text-sm/6"
		>
			<p>&copy; 2023-{new Date().getFullYear()} Michael Bonner</p>
			<a
				href="https://michaelbonner.dev/"
				class="font-normal text-emerald-800 underline decoration-emerald-600/50 underline-offset-4"
				>michaelbonner.dev</a
			>
		</div>
	</footer>
</main>
