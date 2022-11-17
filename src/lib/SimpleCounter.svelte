<script lang="ts">
import { onMount } from 'svelte';
export let value: number;
export const delay: number = 100;
export const transitionDuration: number = 1000;
export const transitionTiming: string = 'ease';
let mounted: boolean = false;
onMount(() => {
	setTimeout(() => {
		mounted = true;
	}, delay);
})
</script>

<span class="counter" style="--num: {mounted ? value : 0}; --duration: {`${transitionDuration}ms`}; --timing: {transitionTiming}"></span>

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
