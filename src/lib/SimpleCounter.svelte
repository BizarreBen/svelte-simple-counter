<script lang="ts">
	import { onMount } from 'svelte';
	import SimpleCSSCounter from './SimpleCSSCounter.svelte';
	import SimpleJSCounter from './SimpleJSCounter.svelte';
	export let prefersCSS: boolean = true;
	export let value: number;
	export let delay: number = 100;
	export let transitionDuration: number = 1000;
	export let transitionTiming: string = 'ease';
	export let customDisplay: null | ((x: number) => any) = null;
	let supported: boolean = true;
	let mounted: boolean = false;

	onMount(async () => {
		supported = CSS.registerProperty !== undefined;
		mounted = true;
	});
</script>

{#if mounted}
	{#if supported && prefersCSS && customDisplay === null}
		<SimpleCSSCounter {value} {delay} {transitionDuration} {transitionTiming} />
	{:else}
		<SimpleJSCounter {value} {delay} {transitionDuration} {transitionTiming} {customDisplay} />
	{/if}
{/if}
