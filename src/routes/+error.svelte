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

<main class="grid min-h-[70vh] place-items-center py-12 text-sky-950">
	<div class="grid w-full max-w-md gap-6 py-10 px-8 text-center bg-white/70 rounded-2xl border">
		<p class="text-6xl font-black tracking-tighter text-sky-700">
			{page.status}
		</p>

		<div class="grid gap-3">
			<h1 class="text-2xl font-bold lg:text-3xl">
				{#if page.status === 404}
					Page not found
				{:else if page.status === 500}
					Something went wrong
				{:else}
					An error occurred
				{/if}
			</h1>

			<p class="text-base font-light text-sky-900/80">
				{#if page.status === 404}
					The page you're looking for doesn't exist or may have been moved.
				{:else if page.error?.message}
					{page.error.message}
				{:else}
					We ran into an unexpected problem. Please try again in a moment.
				{/if}
			</p>
		</div>

		<div class="flex flex-col items-center gap-3 sm:flex-row sm:justify-center">
			<a
				href={resolve('/')}
				class="inline-flex w-full items-center justify-center gap-2 rounded-lg bg-sky-700 px-6 py-3 text-sm font-semibold text-white transition-colors hover:bg-sky-800 sm:w-auto"
			>
				Back to home
			</a>
			<button
				type="button"
				onclick={() => history.back()}
				class="inline-flex w-full items-center justify-center gap-2 rounded-lg border border-sky-200 bg-white/70 px-6 py-3 text-sm font-semibold text-sky-900 transition-colors hover:bg-white sm:w-auto"
			>
				Go back
			</button>
		</div>
	</div>
</main>
