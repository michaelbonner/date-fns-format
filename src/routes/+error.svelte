<script lang="ts">
	import { page } from '$app/state';
	import { resolve } from '$app/paths';
</script>

<svelte:head>
	<title>
		{page.status === 404 ? 'Page Not Found' : `Error ${page.status}`} | date-fns format helper
	</title>
	<meta name="robots" content="noindex" />
</svelte:head>

<div class="isolate flex min-h-dvh flex-col">
	<header class="border-b border-white/10 bg-[#102f2b] text-[#f7f5ef]">
		<div class="mx-auto flex max-w-7xl items-center justify-between gap-6 px-5 py-5 sm:px-8">
			<a href={resolve('/')} aria-label="Homepage" class="font-semibold tracking-tight"
				>date-fns / format</a
			>
		</div>
	</header>

	<main class="grid flex-1 items-center py-12 sm:py-16">
		<div class="mx-auto w-full max-w-7xl px-5 sm:px-8">
			<div class="max-w-xl border-l-4 border-emerald-600 bg-[#e7efe9] p-6 sm:p-8">
				<p class="font-mono text-base/7 text-emerald-800 sm:text-sm/6">Error {page.status}</p>

				<h1
					class="mt-3 text-4xl font-semibold tracking-tight text-balance text-[#1c2528] sm:text-5xl"
				>
					{#if page.status === 404}
						Page not found
					{:else if page.status === 500}
						Something went wrong
					{:else}
						An error occurred
					{/if}
				</h1>

				<p class="mt-4 max-w-[52ch] text-lg/8 text-pretty text-[#526064] sm:text-base/7">
					{#if page.status === 404}
						The page you're looking for doesn't exist or may have been moved.
					{:else if page.error?.message}
						{page.error.message}
					{:else}
						We ran into an unexpected problem. Please try again in a moment.
					{/if}
				</p>

				<div class="mt-6 flex flex-wrap items-center gap-3">
					<a
						href={resolve('/')}
						class="rounded-md bg-emerald-700 px-3.5 py-2 text-base/6 font-medium text-white ring-1 ring-emerald-700 hover:bg-emerald-800 focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-emerald-700 sm:text-sm/5"
					>
						Back to home
					</a>
					<button
						type="button"
						onclick={() => history.back()}
						class="rounded-md px-3.5 py-2 text-base/6 font-medium text-emerald-800 ring-1 ring-emerald-800/25 hover:bg-white/60 focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-emerald-700 sm:text-sm/5"
					>
						Go back
					</button>
				</div>
			</div>
		</div>
	</main>
</div>
