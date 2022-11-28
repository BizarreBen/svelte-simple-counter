<script lang="ts">
	import { onMount } from 'svelte';
	export let value: number;
	export let delay: number = 100;
	export let transitionDuration: number = 1000;
	export let transitionTiming: string = 'ease';
	let mounted: boolean = false;
	onMount(() => {
		setTimeout(() => {
			mounted = true;
		}, delay);
	});
</script>

<span
	class="counter"
	style="--num: {mounted
		? value
		: 0}; --duration: {`${transitionDuration}ms`}; --timing: {transitionTiming}"
/>

<style>
	@property --num {
		syntax: '<integer>';
		initial-value: 0;
		inherits: false;
	}

	.counter {
		transition: --num var(--duration) var(--timing);
		counter-reset: num var(--num);
	}

	.counter::after {
		content: counter(num);
	}
</style>
