<script lang="ts">
    import { onMount } from 'svelte';
    import SimpleCSSCounter from './SimpleCSSCounter.svelte';
    import SimpleJSCounter from './SimpleJSCounter.svelte';
    const css = "@property --num { \
		syntax: '<integer>'; \
		initial-value: 0; \
		inherits: false; \
	}";
    export let prefersCSS: boolean = true;
	export let value: number;
	export let delay: number = 100;
	export let transitionDuration: number = 1000;
	export let transitionTiming: string = 'ease';
    let supported: boolean = true;
    let mounted: boolean = false;

    onMount(async () => {
        supported = CSS.supports('at-rule(@property)');
        mounted = true;
    })
</script>
{#if mounted}
    {#if supported && prefersCSS}
    <SimpleCSSCounter value={value} delay={delay} transitionDuration={transitionDuration} transitionTiming={transitionTiming} />
    {:else}
    <SimpleJSCounter value={value} delay={delay} transitionDuration={transitionDuration} transitionTiming={transitionTiming} />
    {/if}
{/if}