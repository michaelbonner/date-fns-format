<script lang="ts">
	import { format } from 'date-fns';

	let now = new Date();

	let testFormat = 'yyyy-MM-dd HH:mm:ss';

	let testFormatDateString = '';

	setInterval(() => {
		now = new Date();

		try {
			testFormatDateString = format(now, testFormat);
		} catch (error) {
			testFormatDateString = 'Invalid format';
		}
	}, 500);

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
	<meta name="theme-color" content="#076971" />
	<meta name="color-scheme" content="light only" />
	<meta
		name="description"
		content="A simple tool to help keep track of commonly used date formats. The tool is also helpful to test custom date formats."
	/>

	<meta property="og:image" content="https://date-fns.michaelbonner.dev/og-image.jpg" />
	<meta property="og:type" content="website" />
	<meta property="og:title" content="date-fns format helper" />

	<meta name="twitter:card" content="summary_large_image" />

	<link rel="canonical" href="https://date-fns.michaelbonner.dev/" />
</svelte:head>

<main class="grid gap-12 py-4">
	<h1 class="text-3xl lg:text-5xl font-bold">date-fns format helper</h1>
	<div class="text-xl">
		<span>Reference Time:</span>
		<span>
			{now.toLocaleDateString()}
			{now.toLocaleTimeString()}
		</span>
	</div>
	<div class="grid gap-4">
		<h2 class="text-2xl lg:text-3xl font-bold">Test</h2>
		<dl class="grid gap-1 border py-3 px-6 bg-white bg-opacity-50 rounded-xl">
			<dt class="text-sm">
				<label>
					<input
						bind:value={testFormat}
						class="border py-2 px-4 text-sm rounded bg-white bg-opacity-50"
						placeholder="Test format string"
						type="text"
					/>
				</label>
			</dt>
			<dd class="font-bold">{testFormatDateString}</dd>
		</dl>
	</div>
	<div class="grid gap-4">
		<h2 class="text-2xl lg:text-3xl font-bold">Useful Formats</h2>

		<div class="grid md:grid-cols-2 xl:grid-cols-3 gap-x-4 gap-y-2">
			{#each formatStrings as formatString}
				<dl class="grid gap-1 py-3 px-6 bg-white bg-opacity-50 rounded-xl">
					<dt class="text-sm">
						<input
							aria-label={`Format string: ${formatString}`}
							disabled
							class="py-1 px-2 italic text-sm border-2 border-dashed border-gray-300 rounded bg-white bg-opacity-50"
							value={formatString}
						/>
					</dt>
					<dd class="font-bold">{format(now, formatString)}</dd>
				</dl>
			{/each}
		</div>
	</div>

	<div>
		Reference: <a class="underline underline-offset-2" href="https://date-fns.org/docs/format"
			>https://date-fns.org/docs/format</a
		>
	</div>

	<div>
		&copy; {new Date().getFullYear()}
		<a class="underline underline-offset-2" href="https://michaelbonner.dev/"> Michael Bonner </a>
	</div>
</main>

<style lang="postcss">
	:global(html) {
		background-color: theme(colors.gray.100);
	}
</style>
