<script lang="ts">
	import { _ } from 'svelte-i18n'
	import { SearchIcon } from '$lib/components/icons'

	export let query = ''
	export let label = ''
	export let placeholder = ''

	let element: HTMLElement

	function handleKeydown(e: KeyboardEvent) {
		if (e.key === 'Escape') {
			element.blur()
		}

		if (
			e.key === '/' &&
			element != null &&
			document.activeElement?.tagName === 'BODY' &&
			document.activeElement !== element
		) {
			e.preventDefault()
			element.focus()
		}
	}
</script>

<svelte:window on:keydown={handleKeydown} />

<div
	class="relative flex h-12 w-full max-w-sm items-center space-x-3 overflow-hidden rounded-full border bg-surface px-3 transition focus-within:ring"
>
	<label for="search">
		<span class="sr-only">{label}</span>
		<span class="text-subtle"><SearchIcon size={20} /></span>
	</label>

	<input
		id="search"
		type="text"
		bind:this={element}
		bind:value={query}
		{placeholder}
		class="h-12 w-full bg-transparent py-3 text-sm font-medium text-text placeholder-muted focus:outline-none sm:h-10"
	/>

	<div
		class="pointer-events-none absolute right-3 flex h-6 items-center rounded-md border border-muted/20 bg-muted/10 px-1.5 font-mono text-[10px] font-medium text-subtle ring-muted/30 ring-offset-1 ring-offset-surface transition hover:bg-muted/20 hover:text-text focus:text-text focus:outline-none focus:ring"
	>
		<kbd>/</kbd>
	</div>
</div>
