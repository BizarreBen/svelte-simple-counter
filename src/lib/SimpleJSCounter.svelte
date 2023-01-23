<script lang="ts">
	import { onMount } from 'svelte';
	import bezier from 'bezier-easing';
	export let value: number;
	export let delay: number = 100;
	export let transitionDuration: number = 1000;
	export let transitionTiming: string = 'ease';
	let computed = 0;
	let prev = 0;
	let easingFunction: bezier.EasingFunction;
	let intervalId: NodeJS.Timer;
	let transitionData: number[];

	export let customDisplay : null | ((x: number) => any) = null;

	function compute() {
		clearInterval(intervalId);
		const start = Date.now();
		prev = computed;
		computed = Math.round(
			prev +
				easingFunction(Math.min((Date.now() - start) / transitionDuration, 1.0)) * (value - prev)
		);
		if (computed === value) return;
		intervalId = setInterval(() => {
			let eased = easingFunction(Math.min((Date.now() - start) / transitionDuration, 1.0));
			computed = Math.round(prev + eased * (value - prev));
			if (eased === 1) {
				clearInterval(intervalId);
				computed = value;
			}
		}, transitionDuration / Math.abs(value - start));
	}

	switch (transitionTiming) {
		case 'ease':
			easingFunction = bezier(0.25, 0.1, 0.25, 1);
			break;
		case 'ease-in':
			easingFunction = bezier(0.42, 0, 1, 1);
			break;
		case 'ease-out':
			easingFunction = bezier(0, 0, 0.58, 1);
			break;
		case 'ease-in-out':
			easingFunction = bezier(0.42, 0, 0.58, 1);
			break;
		case 'linear':
			easingFunction = bezier(0, 0, 1, 1);
			break;
		default:
			if (!transitionTiming.startsWith('cubic-bezier')) {
				easingFunction = bezier(0.25, 0.1, 0.25, 1);
				break;
			}
			transitionData = transitionTiming
				.replace(/[^\d.,]/g, '')
				.split(',')
				.map((x) => parseFloat(x));
			easingFunction = bezier(
				transitionData[0],
				transitionData[1],
				transitionData[2],
				transitionData[3]
			);
			break;
	}

	$: value, compute();
	onMount(() => {
		setTimeout(() => {
			compute();
		}, delay);
	});
</script>

<span class="counter">{customDisplay != null ? customDisplay(computed) : computed}</span>
