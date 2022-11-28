<script>
	import SimpleCounter from '$lib/SimpleCounter.svelte';
	let numbah = 0;
	setInterval(() => {
		numbah = Math.ceil(Math.random() * 10000);
	}, 10000);
</script>

<h1>Welcome to your library project</h1>
<p>Create your package using @sveltejs/package and preview/showcase your work with SvelteKit</p>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>

<div>{numbah}</div>
<SimpleCounter value={numbah} delay={200} transitionDuration={5000} transitionTiming={'cubic-bezier(.2,.71,.13,1.66)'} />
