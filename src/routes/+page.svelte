<script>
    import SimpleCounter from '$lib/SimpleCounter.svelte';
    let numbah = 0;
    setInterval(() => {
        numbah = Math.ceil(Math.random() * 10000);
    }, 5000);
</script>
<h1>Welcome to your library project</h1>
<p>Create your package using @sveltejs/package and preview/showcase your work with SvelteKit</p>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>

<SimpleCounter num={numbah} delay={200} transitionDuration={500} transitionTiming={'ease-out'} />